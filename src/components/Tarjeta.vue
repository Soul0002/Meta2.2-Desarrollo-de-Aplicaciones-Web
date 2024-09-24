<template>
  <v-card
    class="mx-auto"
    max-width="344"
  >
    <v-img
      height="200px"
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      cover
    ></v-img>

    <v-card-title>
      Sí señor, yo soy de rancho
    </v-card-title>

    <v-card-subtitle>
      De botas y a caballo
    </v-card-subtitle>

    <v-card-actions>
      <v-btn
        color="orange-lighten-2"
        text="Explore"
      ></v-btn>

      <v-spacer></v-spacer>

      <v-btn
        :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show = !show"
      ></v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>

  <v-container class="d-flex justify-center">  
        <v-col cols="12" md="4" sm="6">
          <v-btn rounded="xl" size="x-large" block onclick= RouterLink to = "/">Página principal

          </v-btn>
        </v-col>
      
    </v-container>
</template>

<script setup>
  import { ref } from "vue";
  const show = ref(false);
</script>