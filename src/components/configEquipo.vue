<template>
    <div>
      <h2>Configuración del Equipo</h2>
      <form @submit.prevent="guardarConfigEquipo">
        <label>
          Virtual:
          <input type="checkbox" v-model="formData.virtual" />
        </label>
  
        <label>
          Físico:
          <input type="checkbox" v-model="formData.fisico" />
        </label>
  
        <label>
          Producción:
          <input type="checkbox" v-model="formData.produccion" />
        </label>
  
        <label>
          Desarrollo:
          <input type="checkbox" v-model="formData.desarrollo" />
        </label>
  
        <label>
          Procesador:
          <input type="text" v-model="formData.procesador" />
        </label>
  
        <label>
          Velocidad:
          <input type="text" v-model="formData.velocidad" />
        </label>
  
        <label>
          Cantidad:
          <input type="number" v-model="formData.cantidad" />
        </label>
  
        <label>
          Memoria RAM:
          <input type="text" v-model="formData.memoriaRam" />
        </label>
  
        <label>
          Disco Duro:
          <input type="number" v-model="formData.discoDuro" />
        </label>
  
        <label>
          Tipo de Servicio:
          <input type="text" v-model="formData.tipoServicio" />
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
          virtual: false,
          fisico: false,
          produccion: false,
          desarrollo: false,
          procesador: '',
          velocidad: '',
          cantidad: 0,
          memoriaRam: '',
          discoDuro: 0,
          tipoServicio: '',
        },
      };
    },
    methods: {
      guardarConfigEquipo() {
        console.log('Configuración del equipo guardada:', this.formData);
        // Lógica adicional para guardar datos
      },
    },
  };
  </script>
  