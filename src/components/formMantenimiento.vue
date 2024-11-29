<template>
  <div>
    <h2>Mantenimientos</h2>
    <form @submit.prevent="agregarMantenimiento">
      <label>
        Tipo de Mantenimiento:
        <select v-model="nuevoMantenimiento.tipo">
          <option value="Preventivo">Preventivo</option>
          <option value="Correctivo">Correctivo</option>
        </select>
      </label>
      <label>
        Fecha:
        <input type="date" v-model="nuevoMantenimiento.fecha" />
      </label>
      <label>
        Realizado Por:
        <input type="text" v-model="nuevoMantenimiento.realizadoPor" />
      </label>
      <label>
        Observaciones:
        <textarea v-model="nuevoMantenimiento.observaciones"></textarea>
      </label>
      <button type="submit">{{ editIndex === null ? 'Agregar' : 'Actualizar' }}</button>
    </form>

    <h3>Historial de Mantenimientos</h3>
    <ul>
      <li v-for="(mantenimiento, index) in mantenimientos" :key="index">
        <span>
          {{ mantenimiento.tipo }} - {{ mantenimiento.fecha }} - {{ mantenimiento.realizadoPor }} <br />
          <strong>Observaciones:</strong> {{ mantenimiento.observaciones }}
        </span>
        <button @click="editarMantenimiento(index)">Editar</button>
        <button @click="eliminarMantenimiento(index)">Eliminar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nuevoMantenimiento: {
        tipo: "Preventivo",
        fecha: "",
        realizadoPor: "",
        observaciones: "",
      },
      mantenimientos: [],
      editIndex: null,
    };
  },
  mounted() {
    // Cargar los mantenimientos desde localStorage cuando se monte el componente
    const savedMantenimientos = JSON.parse(localStorage.getItem("mantenimientos"));
    if (savedMantenimientos) {
      this.mantenimientos = savedMantenimientos;
    }
  },
  methods: {
    agregarMantenimiento() {
      if (this.editIndex === null) {
        this.mantenimientos.push({ ...this.nuevoMantenimiento });
      } else {
        this.mantenimientos[this.editIndex] = { ...this.nuevoMantenimiento };
        this.editIndex = null;
      }
      this.resetFormulario();
    },
    editarMantenimiento(index) {
      this.nuevoMantenimiento = { ...this.mantenimientos[index] };
      this.editIndex = index;
    },
    eliminarMantenimiento(index) {
      this.mantenimientos.splice(index, 1);
    },
    resetFormulario() {
      this.nuevoMantenimiento = {
        tipo: "Preventivo",
        fecha: "",
        realizadoPor: "",
        observaciones: "",
      };
    },
    guardarMantenimientos() {
      // Guardar los mantenimientos en localStorage
      localStorage.setItem("mantenimientos", JSON.stringify(this.mantenimientos));
    },
  },
};
</script>
