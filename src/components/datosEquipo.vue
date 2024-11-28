<template>
  <div>
    <h2>Datos del Equipo</h2>
    <form @submit.prevent="guardarDatosEquipo">
      <label>
        Fecha:
        <input type="date" v-model="formData.fecha" />
      </label>
      <label>
        Código de Inventario:
        <input type="text" v-model="formData.codigoInventario" />
      </label>
      <label>
        Marca:
        <input type="text" v-model="formData.marca" />
      </label>
      <label>
        Modelo:
        <input type="text" v-model="formData.modelo" />
      </label>
      <label>
        Serial:
        <input type="text" v-model="formData.serial" />
      </label>
      <label>
        Función del Equipo:
        <input type="text" v-model="formData.funcion" />
      </label>
      <button type="submit">Guardar</button>
    </form>

    <h3>Registros</h3>
    <ul>
      <li v-for="(equipo, index) in registros" :key="index">
        <span>{{ equipo.codigoInventario }} - {{ equipo.marca }} - {{ equipo.modelo }}</span>
        <button @click="editar(index)">Editar</button>
        <button @click="eliminar(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        fecha: "",
        codigoInventario: "",
        marca: "",
        modelo: "",
        serial: "",
        funcion: "",
      },
      registros: [],
      editIndex: null,
    };
  },
  methods: {
    guardarDatosEquipo() {
      if (this.editIndex === null) {
        // Agregar nuevo registro
        this.registros.push({ ...this.formData });
      } else {
        // Modificar registro existente
        this.registros[this.editIndex] = { ...this.formData };
        this.editIndex = null;
      }
      this.resetFormulario();
    },
    editar(index) {
      this.formData = { ...this.registros[index] };
      this.editIndex = index;
    },
    eliminar(index) {
      this.registros.splice(index, 1);
    },
    resetFormulario() {
      this.formData = {
        fecha: "",
        codigoInventario: "",
        marca: "",
        modelo: "",
        serial: "",
        funcion: "",
      };
    },
  },
};
</script>
