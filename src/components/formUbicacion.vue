<template>
  <div>
    <h2>Ubicaciones</h2>
    <form @submit.prevent="agregarFila">
      <label>
        Área/Dependencia:
        <input type="text" v-model="nuevaFila.area" />
      </label>
      <label>
        Responsable:
        <input type="text" v-model="nuevaFila.responsable" />
      </label>
      <label>
        Fecha de Instalación/Traslado:
        <input type="date" v-model="nuevaFila.fechaInstalacion" />
      </label>
      <button type="submit">{{ editIndex === null ? 'Agregar' : 'Actualizar' }}</button>
    </form>

    <h3>Ubicaciones Registradas</h3>
    <ul>
      <li v-for="(fila, index) in filas" :key="index">
        <span>{{ fila.area }} - {{ fila.responsable }} - {{ fila.fechaInstalacion }}</span>
        <button @click="editarFila(index)">Editar</button>
        <button @click="eliminarFila(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevaFila: {
        area: "",
        responsable: "",
        fechaInstalacion: "",
      },
      filas: [],
      editIndex: null,
    };
  },
  mounted() {
    // Cargar las filas desde localStorage cuando el componente se monte
    const savedFilas = JSON.parse(localStorage.getItem("ubicaciones"));
    if (savedFilas) {
      this.filas = savedFilas;
    }
  },
  methods: {
    agregarFila() {
      if (this.editIndex === null) {
        this.filas.push({ ...this.nuevaFila });
      } else {
        this.filas[this.editIndex] = { ...this.nuevaFila };
        this.editIndex = null;
      }
      this.resetFila();
    },
    editarFila(index) {
      this.nuevaFila = { ...this.filas[index] };
      this.editIndex = index;
    },
    eliminarFila(index) {
      this.filas.splice(index, 1);
    },
    resetFila() {
      this.nuevaFila = {
        area: "",
        responsable: "",
        fechaInstalacion: "",
      };
    },
    guardarFilas() {
      // Guardar las filas en localStorage
      localStorage.setItem("ubicaciones", JSON.stringify(this.filas));
    },
  },
};
</script>
