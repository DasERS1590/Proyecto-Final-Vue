<template>
  <div>
    <!-- Sistemas Operativos -->
    <div>
      <h2>Sistemas Operativos</h2>
      <form @submit.prevent="agregarFilaSistema">
        <label>
          Descripción:
          <input type="text" v-model="nuevaFilaSistema.descripcion" />
        </label>
        <label>
          Sistema Operativo:
          <input type="text" v-model="nuevaFilaSistema.sistemaOperativo" />
        </label>
        <label>
          Versión:
          <input type="text" v-model="nuevaFilaSistema.version" />
        </label>
        <label>
          Licencia:
          <input type="text" v-model="nuevaFilaSistema.licencia" />
        </label>
        <label>
          Fecha:
          <input type="date" v-model="nuevaFilaSistema.fecha" />
        </label>
        <button type="submit">{{ editIndexSistema === null ? 'Agregar' : 'Actualizar' }}</button>
      </form>

      <h3>Lista de Sistemas Operativos</h3>
      <table border="1">
        <thead>
          <tr>
            <th>Nro.</th>
            <th>Descripción</th>
            <th>Sistema Operativo</th>
            <th>Versión</th>
            <th>Licencia</th>
            <th>Fecha</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(fila, index) in filasSistema" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ fila.descripcion }}</td>
            <td>{{ fila.sistemaOperativo }}</td>
            <td>{{ fila.version }}</td>
            <td>{{ fila.licencia }}</td>
            <td>{{ fila.fecha }}</td>
            <td>
              <button @click="editarFilaSistema(index)">Editar</button>
              <button @click="eliminarFilaSistema(index)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- Aplicaciones -->
    <div>
      <h2>Aplicaciones</h2>
      <form @submit.prevent="agregarFilaAplicacion">
        <label>
          Descripción:
          <input type="text" v-model="nuevaFilaAplicacion.descripcion" />
        </label>
        <label>
          Aplicación:
          <input type="text" v-model="nuevaFilaAplicacion.aplicacion" />
        </label>
        <label>
          Versión:
          <input type="text" v-model="nuevaFilaAplicacion.version" />
        </label>
        <label>
          Licencia:
          <input type="text" v-model="nuevaFilaAplicacion.licencia" />
        </label>
        <label>
          Fecha:
          <input type="date" v-model="nuevaFilaAplicacion.fecha" />
        </label>
        <button type="submit">{{ editIndexAplicacion === null ? 'Agregar' : 'Actualizar' }}</button>
      </form>

      <h3>Lista de Aplicaciones</h3>
      <table border="1">
        <thead>
          <tr>
            <th>Nro.</th>
            <th>Descripción</th>
            <th>Aplicación</th>
            <th>Versión</th>
            <th>Licencia</th>
            <th>Fecha</th>
            <th>Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(fila, index) in filasAplicacion" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ fila.descripcion }}</td>
            <td>{{ fila.aplicacion }}</td>
            <td>{{ fila.version }}</td>
            <td>{{ fila.licencia }}</td>
            <td>{{ fila.fecha }}</td>
            <td>
              <button @click="editarFilaAplicacion(index)">Editar</button>
              <button @click="eliminarFilaAplicacion(index)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // Sistemas Operativos
      nuevaFilaSistema: {
        descripcion: "",
        sistemaOperativo: "",
        version: "",
        licencia: "",
        fecha: "",
      },
      filasSistema: [],
      editIndexSistema: null,

      // Aplicaciones
      nuevaFilaAplicacion: {
        descripcion: "",
        aplicacion: "",
        version: "",
        licencia: "",
        fecha: "",
      },
      filasAplicacion: [],
      editIndexAplicacion: null,
    };
  },
  methods: {
    // Métodos para Sistemas Operativos
    agregarFilaSistema() {
      if (this.editIndexSistema === null) {
        this.filasSistema.push({ ...this.nuevaFilaSistema });
      } else {
        this.filasSistema[this.editIndexSistema] = { ...this.nuevaFilaSistema };
        this.editIndexSistema = null;
      }
      this.resetFilaSistema();
    },
    editarFilaSistema(index) {
      this.nuevaFilaSistema = { ...this.filasSistema[index] };
      this.editIndexSistema = index;
    },
    eliminarFilaSistema(index) {
      this.filasSistema.splice(index, 1);
    },
    resetFilaSistema() {
      this.nuevaFilaSistema = {
        descripcion: "",
        sistemaOperativo: "",
        version: "",
        licencia: "",
        fecha: "",
      };
    },

    // Métodos para Aplicaciones
    agregarFilaAplicacion() {
      if (this.editIndexAplicacion === null) {
        this.filasAplicacion.push({ ...this.nuevaFilaAplicacion });
      } else {
        this.filasAplicacion[this.editIndexAplicacion] = { ...this.nuevaFilaAplicacion };
        this.editIndexAplicacion = null;
      }
      this.resetFilaAplicacion();
    },
    editarFilaAplicacion(index) {
      this.nuevaFilaAplicacion = { ...this.filasAplicacion[index] };
      this.editIndexAplicacion = index;
    },
    eliminarFilaAplicacion(index) {
      this.filasAplicacion.splice(index, 1);
    },
    resetFilaAplicacion() {
      this.nuevaFilaAplicacion = {
        descripcion: "",
        aplicacion: "",
        version: "",
        licencia: "",
        fecha: "",
      };
    },
  },
};
</script>
