<template>
  <div>
    <h2>Mantenimiento</h2>
    <form @submit.prevent="guardarMantenimiento">
      <label>
        Tipo de Mantenimiento:
        <select v-model="formData.tipo">
          <option value="preventivo">Preventivo</option>
          <option value="correctivo">Correctivo</option>
        </select>
      </label>

      <label>
        Fecha:
        <input type="date" v-model="formData.fecha" />
      </label>

      <label>
        Realizó:
        <input type="text" v-model="formData.realizo" />
      </label>

      <label>
        Observaciones:
        <textarea v-model="formData.observaciones"></textarea>
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
        tipo: '',
        fecha: '',
        realizo: '',
        observaciones: '',
      },
    };
  },
  methods: {
    guardarMantenimiento() {
      console.log('Mantenimiento guardado:', this.formData);
      // Lógica adicional para guardar datos
    },
  },
};
</script>

<script>
export default {
  name: 'FormMantenimiento',
};
</script>
