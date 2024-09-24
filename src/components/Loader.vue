<!-- Loader.vue -->
<template>
    <v-container>
      <!-- Mostrar alertas de error -->
      <v-alert
        v-if="errorMessage"
        type="error"
        dismissible
        @input="clearError"
      >
        {{ errorMessage }}
      </v-alert>
  
      <!-- Progreso circular o linear para indicar carga -->
      <v-progress-circular
      v-if="loading"
        indeterminate
      ></v-progress-circular>
  
      <!-- Alternativamente, progreso linear -->
      <v-progress-linear
        v-if="loading"
        indeterminate
      ></v-progress-linear>
    </v-container>
  </template>
  
  <script>
  export default {
    props: {
      loading: {
        type: Boolean,
        default: false
      },
      errorMessage: {
        type: String,
        default: ''
      }
    },
    methods: {
      clearError() {
        this.$emit('clear-error'); // Emitir evento para limpiar el error
      }
    }
  };
  </script>
  