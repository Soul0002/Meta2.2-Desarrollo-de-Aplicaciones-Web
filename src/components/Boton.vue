<template>
    <v-container class="d-flex">  
        <v-col cols="12" md="4" sm="6">
          <v-btn rounded="xl" size="x-large" block @click="refreshPage()" >Cambiar imagen
          </v-btn>
        </v-col>
      
    </v-container>
  </template>

<script>
export default {
  methods: {
    refreshPage() {
      // Recargar la página actual
      window.location.reload();
    }
  }
};
</script>