<template>
    <div>
      <h2>Configuración de Red</h2>
      <form @submit.prevent="guardarConfigRed">
        <label>
          Nombre del Equipo:
          <input type="text" v-model="formData.nombreEquipo" />
        </label>
  
        <label>
          Dirección IP Privada:
          <input type="text" v-model="formData.ipPrivada" />
        </label>
  
        <label>
          Dirección IP Pública:
          <input type="text" v-model="formData.ipPublica" />
        </label>
  
        <label>
          Dominio de Red:
          <input type="text" v-model="formData.dominioRed" />
        </label>
  
        <button type="submit">Guardar</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        formData: {
          nombreEquipo: '',
          ipPrivada: '',
          ipPublica: '',
          dominioRed: '',
        },
      };
    },
    methods: {
      guardarConfigRed() {
        console.log('Configuración de red guardada:', this.formData);
        // Lógica adicional para guardar datos
      },
    },
  };
  </script>
  