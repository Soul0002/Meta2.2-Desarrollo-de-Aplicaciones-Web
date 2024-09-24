<template>
  <v-container>
    <!-- Mostrar el título seleccionado en la parte superior -->
    <v-alert>
      Película seleccionada: <strong>{{ selectedMovie }}</strong>
    </v-alert>
    <!-- Alerta para mostrar errores -->
    <v-alert
      v-if="errorMessage"
      type="error"
      dismissible
    >
      {{ errorMessage }}
    </v-alert>
    <v-table>
      <thead>
        <tr>
          <th>Título</th>
          <th>Calificación</th>
          <th>IMDB</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(movie, index) in movies" :key="index">
          <td @click="selectMovie(movie.movie)" class="movie-title">
            {{ movie.movie }}
          </td>
          <td>{{ movie.rating }}</td>
          <td><a :href="movie.imdb_url" target="_blank">{{ movie.imdb_url }}</a></td>
          <td>
            <v-icon @click="openEditDialog(index)">mdi-pencil</v-icon>
            <v-icon @click="openDeleteDialog(index)" class="ml-2">mdi-delete</v-icon>
          </td>
        </tr>
      </tbody>
    </v-table>

    <!-- Diálogo para editar la película -->
    <v-dialog v-model="editDialog" max-width="500">
      <v-card>
        <v-card-title class="headline">Editar película</v-card-title>
        <v-card-text>
          <v-form>
            <v-text-field
              label="Id"
              v-model="editedMovie.id"
              readonly
            ></v-text-field>

            <v-text-field
              label="Movie"
              v-model="editedMovie.movie"
              required
            ></v-text-field>

            <v-text-field
              label="Rating"
              v-model="editedMovie.rating"
              required
              type="number"
              step="0.1"
              min="0"
              max="10"
            ></v-text-field>

            <v-text-field
              label="IMDB URL"
              v-model="editedMovie.imdb_url"
              required
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="closeEditDialog">Cancelar</v-btn>
          <v-btn @click="saveEdit">Guardar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- Diálogo de confirmación antes de eliminar -->
    <v-dialog v-model="deleteDialog" max-width="400">
      <v-card>
        <v-card-title class="headline">Confirmar eliminación</v-card-title>
        <v-card-text>
          ¿Estás seguro de que deseas eliminar la película "<strong>{{ movieToDelete?.movie }}</strong>"?
        </v-card-text>
        <v-card-actions>
          <v-btn @click="closeDeleteDialog">Cancelar</v-btn>
          <v-btn @click="confirmDelete">Eliminar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      movies: [],
      selectedMovie: null, // Para almacenar la película seleccionada
      editDialog: false, // Controla si el diálogo de edición está abierto o cerrado
      deleteDialog: false, // Controla si el diálogo de eliminación está abierto o cerrado
      editedMovie: {}, // Almacena la película que se está editando
      movieToDelete: null, // Almacena la película que se quiere eliminar
    };
  },
  mounted() {
    this.fetchMovies();
  },
  methods: {
    async fetchMovies() {
      try {
    const response = await axios.get('https://dummyapi.online/api/movies');
    this.movies = response.data;
    this.errorMessage = "";
  } catch (error) {
    if (!error.response) {
      console.log("Error de conexión.")
      this.errorMessage = "Error de conexión.";
    }
  }
},
    selectMovie(title) {
      this.selectedMovie = title;
    },
    openEditDialog(index) {
      // Cargar la película seleccionada en el formulario de edición
      this.editedMovie = { ...this.movies[index] };
      this.editDialog = true;
    },
    closeEditDialog() {
      this.editDialog = false;
    },
    saveEdit() {
      // Buscar la película y actualizarla
      const index = this.movies.findIndex((movie) => movie.id === this.editedMovie.id);
      if (index !== -1) {
        this.movies[index] = { ...this.editedMovie };
      }
      this.closeEditDialog();
    },
    openDeleteDialog(index) {
      this.movieToDelete = this.movies[index];
      this.deleteDialog = true;
    },
    closeDeleteDialog() {
      this.deleteDialog = false;
    },
    confirmDelete() {
      const index = this.movies.indexOf(this.movieToDelete);
      if (index > -1) {
        this.movies.splice(index, 1);
      }
      this.closeDeleteDialog();
    },
  },
};
</script>
