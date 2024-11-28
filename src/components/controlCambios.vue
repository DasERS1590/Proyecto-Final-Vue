<template>
  <div>
    <h2>Sistemas Operativos</h2>
    <form @submit.prevent="agregarFila">
      <label>
        Descripción:
        <input type="text" v-model="nuevaFila.descripcion" />
      </label>
      <label>
        Sistema Operativo:
        <input type="text" v-model="nuevaFila.sistemaOperativo" />
      </label>
      <label>
        Versión:
        <input type="text" v-model="nuevaFila.version" />
      </label>
      <label>
        Fecha:
        <input type="date" v-model="nuevaFila.fecha" />
      </label>
      <button type="submit">Agregar</button>
    </form>

    <h3>Filas</h3>
    <ul>
      <li v-for="(fila, index) in filas" :key="index">
        <span>{{ fila.descripcion }} - {{ fila.sistemaOperativo }} - {{ fila.version }}</span>
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
        descripcion: "",
        sistemaOperativo: "",
        version: "",
        fecha: "",
      },
      filas: [],
      editIndex: null,
    };
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
        descripcion: "",
        sistemaOperativo: "",
        version: "",
        fecha: "",
      };
    },
  },
};
</script>
