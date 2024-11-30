<template>
  <div class="doc_cb">
    <h4 class="title_cb">4. Control de cambios</h4>

      <section class="conf_so">

        <h3 class="title_so">4.1 Control de cambios</h3>

        <form @submit.prevent="agregarFilaSistema">

          <div class="datos_so">

            <div class="input-group flex-nowrap">
              <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Descripción:</span>
              <input type="text" class="form-control border border-dark" aria-label="Username"
                aria-describedby="addon-wrapping" v-model="nuevaFilaSistema.descripcion">
            </div>

            <div class="input-group flex-nowrap">
              <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Sistema operativo:</span>
              <input v-model="nuevaFilaSistema.sistemaOperativo" type="text" class="form-control border border-dark"
                aria-label="Username" aria-describedby="addon-wrapping">
            </div>

            <div class="input-group flex-nowrap">
              <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Versión:</span>
              <input v-model="nuevaFilaSistema.version" type="text" class="form-control border border-dark"
                aria-label="Username" aria-describedby="addon-wrapping">
            </div>

            <div class="input-group flex-nowrap">
              <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Licencia:</span>
              <input v-model="nuevaFilaSistema.licencia" type="text" class="form-control border border-dark"
                aria-label="Username" aria-describedby="addon-wrapping">
            </div>

            <div class="input-group flex-nowrap">
              <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Fecha:</span>
              <input v-model="nuevaFilaSistema.fecha" type="date" class="form-control border border-dark"
                aria-label="Username" aria-describedby="addon-wrapping">
            </div>

          </div>


          <button class="btn btn-success" id="btn_so" type="submit">{{ editIndexSistema === null ? 'Agregar' :
            'Actualizar' }}</button>

        </form>

      </section>

      <div class="separe4"></div>

      <section class="list_so">

        <h3 class="title_list_so">Lista de Sistemas Operativos</h3>


        <div class="gest_table">

          <table class="table table-striped border-dark">
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
            <tbody class="tab_filas">
              <tr v-for="(fila, index) in filasSistema" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ fila.descripcion }}</td>
                <td>{{ fila.sistemaOperativo }}</td>
                <td>{{ fila.version }}</td>
                <td>{{ fila.licencia }}</td>
                <td>{{ fila.fecha }}</td>

                <td class="btn_reg">
                  <a @click="editarFilaSistema(index)" class="btn_edit btn btn-secondary">

                    <i class="fa-solid fa-square-pen"></i>

                  </a>

                  <a @click="eliminarFilaSistema(index)" class="btn_delete btn btn-danger">
                    <i class="fa-solid fa-square-xmark"></i>
                  </a>
                </td>
              </tr>
            </tbody>
          </table>

        </div>


      </section>


    <section class="conf_app">

      <form @submit.prevent="agregarFilaAplicacion">

        <h3 class="title_app">4.2 Aplicaciones</h3>

        <div class="datos_app">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Descripción:</span>
            <input type="text" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping" v-model="nuevaFilaAplicacion.descripcion">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Aplicación:</span>
            <input v-model="nuevaFilaAplicacion.sistemaOperativo" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Versión:</span>
            <input v-model="nuevaFilaAplicacion.version" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Licencia:</span>
            <input v-model="nuevaFilaAplicacion.licencia" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Fecha:</span>
            <input v-model="nuevaFilaAplicacion.fecha" type="date" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

        </div>


        <button class="btn btn-success" id="btn_app" type="submit">{{ editIndexSistema === null ? 'Agregar' :
          'Actualizar' }}</button>

      </form>

    </section>


    <section class="list_app">

      <h3 class="title_list_app">Lista de aplicaciones</h3>

      <div class="gest_table">


        <table class="table table-striped border-dark">
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
          <tbody class="tab_filas">
            <tr v-for="(fila, index) in filasAplicacion" :key="index">
              <td>{{ index + 1 }}</td>
              <td>{{ fila.descripcion }}</td>
              <td>{{ fila.aplicacion }}</td>
              <td>{{ fila.version }}</td>
              <td>{{ fila.licencia }}</td>
              <td>{{ fila.fecha }}</td>

              <td class="btn_reg">
                <a @click="editarFilaAplicacion(index)" class="btn_edit btn btn-secondary">

                  <i class="fa-solid fa-square-pen"></i>

                </a>

                <a @click="eliminarFilaAplicacion(index)" class="btn_delete btn btn-danger">
                  <i class="fa-solid fa-square-xmark"></i>
                </a>
              </td>
            </tr>
          </tbody>
        </table>


      </div>

    </section>

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
    mounted() {
      // Cargar datos almacenados en localStorage cuando se monte el componente
      const savedSistemas = JSON.parse(localStorage.getItem("sistemasOperativos"));
      const savedAplicaciones = JSON.parse(localStorage.getItem("aplicaciones"));

      if (savedSistemas) {
        this.filasSistema = savedSistemas;
      }
      if (savedAplicaciones) {
        this.filasAplicacion = savedAplicaciones;
      }
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
        this.guardarSistemas();
        this.resetFilaSistema();
      },
      editarFilaSistema(index) {
        this.nuevaFilaSistema = { ...this.filasSistema[index] };
        this.editIndexSistema = index;
      },
      eliminarFilaSistema(index) {
        this.filasSistema.splice(index, 1);
        this.guardarSistemas();
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
      guardarSistemas() {
        // Guardar en localStorage
        localStorage.setItem("sistemasOperativos", JSON.stringify(this.filasSistema));
      },

      // Métodos para Aplicaciones
      agregarFilaAplicacion() {
        if (this.editIndexAplicacion === null) {
          this.filasAplicacion.push({ ...this.nuevaFilaAplicacion });
        } else {
          this.filasAplicacion[this.editIndexAplicacion] = { ...this.nuevaFilaAplicacion };
          this.editIndexAplicacion = null;
        }
        this.guardarAplicaciones();
        this.resetFilaAplicacion();
      },
      editarFilaAplicacion(index) {
        this.nuevaFilaAplicacion = { ...this.filasAplicacion[index] };
        this.editIndexAplicacion = index;
      },
      eliminarFilaAplicacion(index) {
        this.filasAplicacion.splice(index, 1);
        this.guardarAplicaciones();
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
      guardarAplicaciones() {
        // Guardar en localStorage
        localStorage.setItem("aplicaciones", JSON.stringify(this.filasAplicacion));
      },
    },
  };
</script>