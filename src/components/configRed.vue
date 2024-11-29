<template>
  <div>
    <h2>Configuración de Red</h2>
    <form @submit.prevent="guardarConfigRed">
      <label>
        Nombre del Equipo:
        <input type="text" v-model="formData.nombreEquipo" />
      </label>

      <fieldset>
        <legend>Direcciones IP Privadas</legend>
        <div v-for="(ip, index) in formData.ipPrivadas" :key="'privada-' + index">
          <input type="text" v-model="formData.ipPrivadas[index]" placeholder="IP Privada" />
          <button type="button" @click="eliminarIP('privada', index)">Eliminar</button>
        </div>
        <button type="button" @click="agregarIP('privada')" :disabled="formData.ipPrivadas.length >= 3">
          Agregar IP Privada
        </button>
      </fieldset>

      <fieldset>
        <legend>Direcciones IP Públicas</legend>
        <div v-for="(ip, index) in formData.ipPublicas" :key="'publica-' + index">
          <input type="text" v-model="formData.ipPublicas[index]" placeholder="IP Pública" />
          <button type="button" @click="eliminarIP('publica', index)">Eliminar</button>
        </div>
        <button type="button" @click="agregarIP('publica')" :disabled="formData.ipPublicas.length >= 3">
          Agregar IP Pública
        </button>
      </fieldset>

      <label>
        Dominio de la Red:
        <input type="text" v-model="formData.dominioRed" />
      </label>

      <button type="submit">{{ editIndex === null ? 'Guardar' : 'Actualizar' }}</button>
    </form>

    <h3>Registros</h3>
    <ul>
      <li v-for="(red, index) in configuraciones" :key="index">
        <span>
          {{ red.nombreEquipo }} - {{ red.dominioRed }} <br />
          <strong>IP Privadas:</strong>
          <ul>
            <li v-for="(ip, ipIndex) in red.ipPrivadas" :key="'privada-' + ipIndex">{{ ip }}</li>
          </ul>
          <strong>IP Públicas:</strong>
          <ul>
            <li v-for="(ip, ipIndex) in red.ipPublicas" :key="'publica-' + ipIndex">{{ ip }}</li>
          </ul>
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
        nombreEquipo: "",
        ipPrivadas: [], // Almacena las IP privadas
        ipPublicas: [], // Almacena las IP públicas
        dominioRed: "",
      },
      configuraciones: [],
      editIndex: null,
    };
  },
  mounted() {
    const savedRedes = JSON.parse(localStorage.getItem("configuracionesRed"));
    if (savedRedes) {
      this.configuraciones = savedRedes;
    }
  },
  methods: {
    agregarIP(tipo) {
      if (tipo === "privada" && this.formData.ipPrivadas.length < 3) {
        this.formData.ipPrivadas.push("");
      } else if (tipo === "publica" && this.formData.ipPublicas.length < 3) {
        this.formData.ipPublicas.push("");
      }
    },
    eliminarIP(tipo, index) {
      if (tipo === "privada") {
        this.formData.ipPrivadas.splice(index, 1);
      } else if (tipo === "publica") {
        this.formData.ipPublicas.splice(index, 1);
      }
      this.guardarConfiguraciones();
    },
    guardarConfigRed() {
      if (this.editIndex === null) {
        this.configuraciones.push({ ...this.formData });
      } else {
        this.configuraciones[this.editIndex] = { ...this.formData };
        this.editIndex = null;
      }
      this.guardarConfiguraciones();
      this.resetFormulario();
    },
    editar(index) {
      this.formData = { ...this.configuraciones[index] };
      this.editIndex = index;
    },
    eliminar(index) {
      this.configuraciones.splice(index, 1);
      this.guardarConfiguraciones();
    },
    guardarConfiguraciones() {
      localStorage.setItem("configuracionesRed", JSON.stringify(this.configuraciones));
    },
    resetFormulario() {
      this.formData = {
        nombreEquipo: "",
        ipPrivadas: [],
        ipPublicas: [],
        dominioRed: "",
      };
    },
  },
};
</script>
