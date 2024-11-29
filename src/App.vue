<template>
  <div id="app">

    <nav class="navbar">
      <div class="container-fluid">
        <h1 href="#">
          Gestion de equipos
        </h1>
      </div>
    </nav>

    <main>

      <component :is="currentComponent" ref="current" />

      <nav class="btn_doc">
        <button class="btn btn-outline-dark" id="btn_ant" @click="prevPage" :disabled="currentIndex === 0">
          Anterior
        </button>
        <button class="btn btn-outline-primary" id="btn_sig" @click="nextPage"
          :disabled="currentIndex === components.length - 1">
          Siguiente
        </button>
      </nav>

    </main>

  </div>

</template>

<script>
import DatosEquipo from "./components/datosEquipo.vue";
import ConfigEquipo from "./components/configEquipo.vue";
import ConfigRed from "./components/configRed.vue";
import ControlCambios from "./components/controlCambios.vue";
import FormUbicacion from "./components/formUbicacion.vue";
import FormMantenimiento from "./components/formMantenimiento.vue";

export default {
  data() {
    return {
      currentIndex: 0,
      components: [
        "DatosEquipo",
        "ConfigEquipo",
        "ConfigRed",
        "ControlCambios",
        "FormUbicacion",
        "FormMantenimiento",
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
      const currentComponent = this.$refs.current; // Referencia al componente actual
      if (currentComponent && currentComponent.guardarRegistros) {
        currentComponent.guardarRegistros(); // Asegura que los datos actuales se guarden
      }
      if (this.currentIndex < this.components.length - 1) {
        this.currentIndex++;
      }
    },
    prevPage() {
      const currentComponent = this.$refs.current;
      if (currentComponent && currentComponent.guardarRegistros) {
        currentComponent.guardarRegistros();
      }
      if (this.currentIndex > 0) {
        this.currentIndex--;
      }
    },
  }
};
</script>

<style>
* {
  font-family: monospace;
}

.navbar {
  margin: 1%;
  border-radius: 10px;
  border: 3px solid rgb(87, 87, 87);
  padding: 1%;
  padding-top: 1.3%;
}

h1 {
  font-family: sans-serif;
  font-weight: bold;
  font-size: 200%;
}

nav {
  margin-top: 20px;
}

.btn_doc {
  margin-top: 5%;
  width: 12.47%;
  margin-left: 86.5%;
}

#btn_ant {
  font-size: 140%;
  margin-right: 5%;
}

#btn_sig {
  font-size: 130%;
}
</style>
