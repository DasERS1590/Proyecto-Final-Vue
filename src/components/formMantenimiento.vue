<template>
  <div>

    <section class="conf_ubi">


      <h3 class="title_ubi">6. Mantenimientos</h3>

      <form @submit.prevent="agregarMantenimiento">

        <div class="datos_ubi">


          <select v-model="nuevoMantenimiento.tipo" class="form-select border border-dark" aria-label="Default select example">
            <option selected>Open this select menu</option>
            <option value="Preventivo">Preventivo</option>
            <option value="Correctivo">Correctivo</option>
          </select>

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Fecha:</span>
            <input v-model="nuevoMantenimiento.fecha" type="date" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>


          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Realizado por:</span>
            <input v-model="nuevoMantenimiento.realizadoPor" type="text" class="form-control border border-dark"
              aria-label="Username" aria-describedby="addon-wrapping">
          </div>

          <div action="" class="func_man">

            <div class="input-group">
              <span class="input-group-text bg-secondary border-dark">Observaciones:</span>
              <textarea v-model="nuevoMantenimiento.observaciones" class="form-control border-dark"
                aria-label="With textarea"></textarea>
            </div>


          </div>

        </div>

        <button class="btn btn-success" id="btn_ubi" type="submit">{{ editIndex === null ? 'Agregar' : 'Actualizar' }}</button>

      </form>



    </section>



    <div class="separe_ubi"></div>


    <section class="list_ubi">

      <h3 class="title_list_ubi">Historial de mantenimientos</h3>

      <div class="gest_table">

        <table class="table tablestriped border-dark">


          <thead>
            <tr>
              <th>|Tipo de mantenimiento|</th>
              <th>|Fecha|</th>
              <th>|Realizado por|</th>
              <th>|Observaciones|</th>
            </tr>
          </thead>

          <tbody class="tab_filas">

            <tr v-for="(mantenimiento, index) in mantenimientos" :key="index">

              <td>{{ mantenimiento.tipo }}</td>
              <td>{{ mantenimiento.fecha }}</td>
              <td>{{ mantenimiento.realizadoPor }}</td>
              <td>{{ mantenimiento.observaciones }}</td>


              <td class="btn_reg">
                <a @click="editarMantenimiento(index)" class="btn_edit btn btn-secondary">

                  <i class="fa-solid fa-square-pen"></i>

                </a>

                <a @click="eliminarMantenimiento(index)" class="btn_delete btn btn-danger">
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
        this.guardarMantenimientos();
        this.resetFormulario();
      },
      editarMantenimiento(index) {
        this.nuevoMantenimiento = { ...this.mantenimientos[index] };
        this.editIndex = index;
      },
      eliminarMantenimiento(index) {
        this.mantenimientos.splice(index, 1);
        this.guardarMantenimientos();
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