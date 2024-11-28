<template>
  <div>
    <h2>Ubicación</h2>
    <form @submit.prevent="guardarUbicacion">
      <label>
        Área/Dependencia:
        <input type="text" v-model="formData.area" />
      </label>

      <label>
        Responsable:
        <input type="text" v-model="formData.responsable" />
      </label>

      <label>
        Fecha de Instalación/Traslado:
        <input type="date" v-model="formData.fecha" />
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
        area: '',
        responsable: '',
        fecha: '',
      },
    };
  },
  methods: {
    guardarUbicacion() {
      console.log('Ubicación guardada:', this.formData);
      // Lógica adicional para guardar datos
    },
  },
};
</script>

<script>
export default {
  name: 'FormUbicacion',
};
</script>
