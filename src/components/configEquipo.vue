<template>
  <div>

    <form @submit.prevent="guardarConfigEquipo">

      <section class="conf_equipo">

        <h5 class="title_conf">
          2. CONFIGURACIÓN DEL EQUIPO:
        </h5>


        <div class="input-group flex-nowrap">

          <div class="chbox">


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


          </div>


        </div>

        <div class="input-group flex-nowrap">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Procesador</span>
          <input v-model="formData.procesador" type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Velocidad</span>
          <input v-model="formData.velocidad" type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Cantidad</span>
          <input type="number" v-model.number="formData.cantidad" @input="validarCantidad"
            class="form-control border border-dark" aria-label="Username" aria-describedby="addon-wrapping">
        </div>

        <div class="input-group flex-nowrap">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Memoria RAM</span>
          <input v-model="formData.memoriaRam" class="form-control border border-dark" id="modf" aria-label="Username"
            aria-describedby="addon-wrapping">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping"></span>
          <input type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">
        </div>



        <div class="part2">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Disco duro</span>

        </div>

        <div class="conf_part3">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Cantidad</span>
          </div>

          <input type="number" v-model="formData.cantDisco" @input="cantDisc" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">

        </div>

        <div action="" class="conf_part4">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Capacidad</span>
          </div>

          <input v-model="formData.capDisco" @input="captDisc" type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">

        </div>

        <div action="" class="conf_part5">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Tipo servicio (Web, BD, <br>
              SAN, AAA, DNS, otro)</span>
            <input v-model="formData.tipoServicio" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

        </div>


        <button class="btn btn-success" type="submit">{{ editIndex === null ? 'Guardar' : 'Actualizar' }}</button>

      </section>

    </form>

    <div class="separe2"></div>


    <section class="register2">


      <h3>Registros</h3>



      <div class="gest_table2">

        <table class="table table-striped border-dark btn-border">

          <thead>
            <th>Modalidad|</th>
            <th>| Estado |</th>
            <th>Procesador|</th>
            <th>Velocidad|</th>
            <th>Cantidad|</th>
            <th>MemoriaRAM |</th>
            <th>Cantidad:HD|</th>
            <th>Capacidad:HD|</th>
            <th>Servicio</th>
          </thead>

          <tbody class="tab_filas">

            <tr v-for="(config, index) in configuraciones" :key="index">

              <td>{{ config.virtual ? 'Virtual' : 'Físico' }}</td>
              <td>{{ config.produccion ? 'Producción' : 'Desarrollo' }}</td>
              <td>{{ config.procesador }}</td>
              <td>{{ config.velocidad }}</td>
              <td>{{ config.cantidad }}</td>
              <td>{{ config.memoriaRam }}</td>
              <td>{{ config.cantDisco }}</td>
              <td>{{ config.capDisco }}</td>
              <td>{{ config.tipoServicio }}</td>



              <td class="btn_reg">
                <a @click="editar(index)" class="btn_edit btn btn-secondary">

                  <i class="fa-solid fa-square-pen"></i>

                </a>

                <a @click="eliminar(index)" class="btn_delete btn btn-danger">
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
        formData: {
          virtual: false,
          fisico: false,
          produccion: false,
          desarrollo: false,
          procesador: '',
          velocidad: '',
          cantidad: 0,
          memoriaRam: '',
          cantDisco: 0,
          capDisco: '',
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
      cantDisc() {
        if (this.formData.cantDisco <= 0) this.formData.cantDisco = 1;
      },
      capDisc() {
        if (this.formData.capDisco <= 0) this.formData.captDisco = false;
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
          cantDisco: 0,
          capDisco:'',
          tipoServicio: '',
        };
      },
    },
  };
</script>