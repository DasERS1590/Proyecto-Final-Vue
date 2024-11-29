<template>
  <div>
    <h2>Configuración del Equipo</h2>
    <form @submit.prevent="guardarConfigEquipo">
      <label>
        Virtual:
        <input type="checkbox" v-model="formData.virtual" @change="toggleVirtualFisico('virtual')" />
      </label>

      <label>
        Físico:
        <input type="checkbox" v-model="formData.fisico" @change="toggleVirtualFisico('fisico')" />
      </label>

      <label>
        Producción:
        <input type="checkbox" v-model="formData.produccion" @change="toggleProduccionDesarrollo('produccion')" />
      </label>

      <label>
        Desarrollo:
        <input type="checkbox" v-model="formData.desarrollo" @change="toggleProduccionDesarrollo('desarrollo')" />
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
        <input type="number" v-model.number="formData.cantidad" @input="validarCantidad" />
      </label>

      <label>
        Memoria RAM:
        <input type="text" v-model="formData.memoriaRam" />
      </label>

      <label>
        Disco Duro:
        <input type="number" v-model.number="formData.discoDuro" @input="validarDiscoDuro" />
      </label>

      <label>
        Tipo de Servicio:
        <input type="text" v-model="formData.tipoServicio" />
      </label>
      <button type="submit">{{ editIndex === null ? 'Guardar' : 'Actualizar' }}</button>
    </form>

    <h3>Registros</h3>
    <ul>
      <li v-for="(config, index) in configuraciones" :key="index">
        <span>
          Virtual o Fisico:{{ config.virtual ? 'Virtual' : 'Físico' }} -
          En Produccion o Desarrollo:{{ config.produccion ? 'Producción' : 'Desarrollo' }} -
          {{ config.procesador }} -
          {{ config.velocidad }} -
          {{ config.cantidad }} -
          {{ config.memoriaRam }} -
          {{ config.discoDuro }}
          {{ config.tipoServicio }} -
        </span>
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
      configuraciones: [],
      editIndex: null,
    };
  },
  mounted() {
    // Cargar los datos almacenados desde localStorage cuando el componente se monte
    const savedConfiguraciones = JSON.parse(localStorage.getItem("configuracionesEquipo"));
    if (savedConfiguraciones) {
      this.configuraciones = savedConfiguraciones;
    }
  },
  methods: {
    toggleVirtualFisico(seleccion) {
      if (seleccion === "virtual") this.formData.fisico = false;
      if (seleccion === "fisico") this.formData.virtual = false;
    },
    toggleProduccionDesarrollo(seleccion) {
      if (seleccion === "produccion") this.formData.desarrollo = false;
      if (seleccion === "desarrollo") this.formData.produccion = false;
    },
    validarCantidad() {
      if (this.formData.cantidad <= 0) this.formData.cantidad = 1;
    },
    validarDiscoDuro() {
      if (this.formData.discoDuro <= 0) this.formData.discoDuro = 1;
    },
    guardarConfigEquipo() {
      if (this.editIndex === null) {
        // Agregar nuevo registro
        this.configuraciones.push({ ...this.formData });
      } else {
        // Modificar registro existente
        this.configuraciones[this.editIndex] = { ...this.formData };
        this.editIndex = null;
      }
      console.log('Configuración del equipo guardada:', this.configuraciones);
      this.resetFormulario();
    },
    editar(index) {
      this.formData = { ...this.configuraciones[index] };
      this.editIndex = index;
    },
    eliminar(index) {
      this.configuraciones.splice(index, 1);
    },
    guardarConfiguraciones() {
      // Guardar las configuraciones en localStorage para persistencia
      localStorage.setItem("configuracionesEquipo", JSON.stringify(this.configuraciones));
    },
    resetFormulario() {
      this.formData = {
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
      };
    },
  },
};
</script>