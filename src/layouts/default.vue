<template>
  <v-app>
    <!-- App bar -->
    <v-app-bar :elevation="2">
      <template v-slot:prepend>
        <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      </template>
      <v-spacer></v-spacer>
      <v-app-bar-title>Meta 2.2 - Consulta y modificación con Vuetify</v-app-bar-title>
    </v-app-bar>

    <!-- Navigation drawer -->
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item title="Drawer layout" subtitle="Hugo Cazarez"></v-list-item>
      <v-divider></v-divider>
      <v-list-item to = '/' link prepend-icon="mdi-view-dashboard" title="Home"></v-list-item>
      <v-list-item to = '/Pagina2' link prepend-icon="mdi-numeric-2-box-multiple-outline" title="Página 2"></v-list-item>
      <v-list-item to = '/peliculas' link prepend-icon="mdi-multimedia" title="Películas"></v-list-item>
    </v-navigation-drawer>

    
    <!-- Main content -->
    <v-main>
      <router-view />
    </v-main>

    <!-- Footer -->
    <AppFooter />
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const drawer = ref(false)
</script>
