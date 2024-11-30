<template>
  <div>

    <section class="datos_equipo">

      <h5 class="title_equipo">
        1. DATOS DEL EQUIPO:
      </h5>

      <!-- Código de inventario -->
      <form action="" class="cod_inv" @submit.prevent="guardarDatosEquipo">
        <div class="input-group flex-nowrap">
          <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Código inventario:</span>
          <input type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping" v-model="formData.codigoInventario">
        </div>

        <!-- Número de ficha -->
        <section class="fcha">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">N° Ficha:</span>
            <input v-model="formData.numeroFicha" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>
          <!-- Fecha -->
          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Fecha:</span>
            <input v-model="formData.fecha" type="date" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping">
          </div>

        </section>

        <section action="" class="datos">
          <!-- Marca, modelo, serial -->

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Marca:</span>
            <input v-model="formData.marca" type="text" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Modelo:</span>
            <input v-model="formData.modelo" type="text" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Serial:</span>
            <input v-model="formData.serial" type="text" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping">
          </div>


        </section>


        <section action="" class="func_equipo">

          <div class="input-group">
            <span class="input-group-text bg-secondary border-dark">Función del equipo</span>
            <textarea v-model="formData.funcion" class="form-control border-dark" aria-label="With textarea"></textarea>
          </div>

          <button class="btn btn-success" type="submit">{{ editIndex === null ? 'Guardar' : 'Actualizar' }}</button>

        </section>


      </form>


    </section>


    <div class="separe"></div>



    <section class="register">


      <h3>Registros</h3>



      <div class="gest_table">

        <table class="table table-striped border-dark btn-border">

          <thead>
            <th># ficha |</th>
            <th>Cod inventario</th>
            <th>|_ Fecha _|</th>
            <th>Marca |</th>
            <th>Modelo |</th>
            <th>serial |</th>
            <th>Función |</th>
          </thead>

          <tbody class="tab_filas">

            <tr v-for="(equipo, index) in registros" :key="index">

              <td>{{ equipo.numeroFicha }}</td>
              <td>{{ equipo.codigoInventario }}</td>
              <td>{{equipo.fecha}}</td>
              <td>{{equipo.marca}}</td>
              <td>{{equipo.modelo}}</td>
              <td>{{equipo.serial}}</td>
              <td>{{equipo.funcion}}</td>
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
          numeroFicha: "",
          fecha: "",
          codigoInventario: "",
          marca: "",
          modelo: "",
          serial: "",
          funcion: "",
        },
        registros: [],
        editIndex: null,
      };
    },
    mounted() {
      // Cargar registros desde localStorage cuando se monte el componente
      const savedRegistros = JSON.parse(localStorage.getItem("registrosEquipos"));
      if (savedRegistros) {
        this.registros = savedRegistros;
      }
    },
    methods: {
      guardarDatosEquipo() {
        if (this.editIndex === null) {
          this.registros.push({ ...this.formData });
        } else {
          this.registros[this.editIndex] = { ...this.formData };
          this.editIndex = null;
        }
        this.guardarRegistros(); // Guarda inmediatamente después de modificar
        this.resetFormulario();
      },
      eliminar(index) {
        this.registros.splice(index, 1);
        this.guardarRegistros(); // Guarda inmediatamente después de eliminar
      },
      resetFormulario() {
        this.formData = {
          numeroFicha: "",
          fecha: "",
          codigoInventario: "",
          marca: "",
          modelo: "",
          serial: "",
          funcion: "",
        };
      },
      guardarRegistros() {
        // Guardar registros en localStorage
        localStorage.setItem("registrosEquipos", JSON.stringify(this.registros));
      },
    },
  };
</script>