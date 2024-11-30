<template>
  <div>


    <section class="conf_ubi">


      <h3 class="title_ubi">5. Ubicaciones</h3>

      <form @submit.prevent="agregarFila">

        <div class="datos_ubi">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Área/Dependecia</span>
            <input v-model="nuevaFila.area" type="text" class="form-control border border-dark" aria-label="Username"
              aria-describedby="addon-wrapping">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Responsable:</span>
            <input v-model="nuevaFila.responsable" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Fecha:</span>
            <input v-model="nuevaFila.fechaInstalacion" type="date" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

        </div>


        <button class="btn btn-success" id="btn_ubi" type="submit">{{ editIndexSistema === null ? 'Actualizar' :
          'Agregar' }}</button>

      </form>


    </section>


    <div class="separe_ubi"></div>


    <section class="list_ubi">

      <h3 class="title_list_ubi">Ubicaciones registradas</h3>


      <div class="gest_table">


        <table class="table table-striped border-dark">


          <thead>
            <tr >
              <th>|Área/Dependencia|</th>
              <th>|Responsable|</th>
              <th>|fecha de instalacion|</th>
              <th>|Acciones|</th>
            </tr>
          </thead>

          <tbody class="tab_filas">

            <tr v-for="(fila, index) in filas" :key="index">

              <td>{{ fila.area }}</td>
              <td>{{ fila.responsable }}</td>
              <td>{{ fila.fechaInstalacion }}</td>


              <td class="btn_reg">
                <a @click="editarFila(index)" class="btn_edit btn btn-secondary">

                  <i class="fa-solid fa-square-pen"></i>

                </a>

                <a @click="eliminarFila(index)" class="btn_delete btn btn-danger">
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
        nuevaFila: {
          area: "",
          responsable: "",
          fechaInstalacion: "",
        },
        filas: [],
        editIndex: null,
      };
    },
    mounted() {
      // Cargar las filas desde localStorage cuando el componente se monte
      const savedFilas = JSON.parse(localStorage.getItem("ubicaciones"));
      if (savedFilas) {
        this.filas = savedFilas;
      }
    },
    methods: {
      agregarFila() {
        if (this.editIndex === null) {
          this.filas.push({ ...this.nuevaFila });
        } else {
          this.filas[this.editIndex] = { ...this.nuevaFila };
          this.editIndex = null;
        }
        this.guardarFilas();
        this.resetFila();
      },
      editarFila(index) {
        this.nuevaFila = { ...this.filas[index] };
        this.editIndex = index;
      },
      eliminarFila(index) {
        this.filas.splice(index, 1);
        this.guardarFilas();
      },
      resetFila() {
        this.nuevaFila = {
          area: "",
          responsable: "",
          fechaInstalacion: "",
        };
      },
      guardarFilas() {
        // Guardar las filas en localStorage
        localStorage.setItem("ubicaciones", JSON.stringify(this.filas));
      },
    },
  };
</script>