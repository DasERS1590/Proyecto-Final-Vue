<template>
  <div id="app">
    <header>
      <h1>Gestión de Equipos</h1>
    </header>
    <main>
      <component :is="currentComponent" />
      <nav>
        <button @click="prevPage" :disabled="currentIndex === 0">Anterior</button>
        <button @click="nextPage" :disabled="currentIndex === components.length - 1">Siguiente</button>
      </nav>
    </main>
  </div>
</template>

<script>
import DatosEquipo from './components/datosEquipo.vue';
import ConfigEquipo from './components/configEquipo.vue';
import ConfigRed from './components/configRed.vue';
import ControlCambios from './components/controlCambios.vue';
import FormUbicacion from './components/formUbicacion.vue';
import FormMantenimiento from './components/formMantenimiento.vue';



export default {
  data() {
    return {
      currentIndex: 0,
      components: [
        'DatosEquipo',
        'ConfigEquipo',
        'ConfigRed',
        'ControlCambios',
        'FormUbicacion',
        'FormMantenimiento',
      ],
    };
  },
  computed: {
    currentComponent() {
      return this.components[this.currentIndex];
    },
  },
  components: {
    DatosEquipo,
    ConfigEquipo,
    ConfigRed,
    ControlCambios,
    FormUbicacion,
    FormMantenimiento,
  },
  methods: {
    nextPage() {
      if (this.currentIndex < this.components.length - 1) {
        this.currentIndex++;
      }
    },
    prevPage() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      }
    },
  },
};
</script>

<style>
/* Añade estilo básico para la navegación */
nav {
  margin-top: 20px;
}
button {
  margin: 5px;
}
</style>
