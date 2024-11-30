<template>
  <div>


    <section class="conf_red">


      <form @submit.prevent="guardarConfigRed">


        <h5 class="title_red">
          3. CONFIGURACIÓN DE RED
        </h5>


        <div action="" class="red_part1">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Nombre del equipo</span>
          </div>

          <input v-model="formData.nombreEquipo" type="text" class="form-control border border-dark"
            aria-label="Username" aria-describedby="addon-wrapping">

        </div>

        <div action="" class="red_part2">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Dirección IP privada</span>
          </div>

          <div v-for="(ip, index) in formData.ipPrivadas" :key="'privada-' + index">
            <input class="form-control border border-dark" type="text" v-model="formData.ipPrivadas[index]"
              placeholder="IP Privada" />
            <button class="btn btn-outline-danger" type="button" @click="eliminarIP('privada', index)">Eliminar</button>
          </div>
          <button class="btn btn-outline-primary" type="button" @click="agregarIP('privada')"
            :disabled="formData.ipPrivadas.length >= 3">
            Agregar IP Privada
          </button>


        </div>

        <div action="" class="red_part3">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Dirección IP pública</span>
          </div>

          <div v-for="(ip, index) in formData.ipPublicas" :key="'publica-' + index">
            <input class="form-control border border-dark" type="text" v-model="formData.ipPublicas[index]"
              placeholder="IP Pública" />
            <button class="btn btn-outline-danger" type="button" @click="eliminarIP('publica', index)">Eliminar</button>
          </div>
          <button class="btn btn-outline-success" type="button" @click="agregarIP('publica')"
            :disabled="formData.ipPublicas.length >= 3">
            Agregar IP Pública
          </button>

        </div>

        <div action="" class="red_part4">

          <div class="input-group flex-nowrap">
            <span class="input-group-text bg-secondary border-dark" id="addon-wrapping">Dominio de red</span>
          </div>

          <input v-model="formData.dominioRed" type="text" class="form-control border border-dark" aria-label="Username"
            aria-describedby="addon-wrapping">

        </div>


        <button class="bt btn btn-success" type="submit">{{ editIndex === null ? 'Guardar' : 'Actualizar' }}</button>


      </form>



    </section>

    <div class="separe3"></div>


    <section class="register3">

      <h3>Registros</h3>

      <div class="gest_table3">

  
        <table class="table table-striped border-dark btn-border">
  
  
          <thead>
            <th>| Nombre equipo |</th>
            <th>| IP privada |</th>
            <th>| IP pública |</th>
            <th>| Dominio de red |</th>
            <th>| Acciones</th>
          </thead>
  
          <tbody class="tab_filas">
  
            <tr v-for="(red, index) in configuraciones" :key="index">
  
  
  
              <td>{{ red.nombreEquipo }}</td>
  
              <td v-for="(ip, ipIndex) in red.ipPrivadas" :key="'privada-' + ipIndex">{{ip}}</td>
  
              <td v-for="(ip, ipIndex) in red.ipPublicas" :key="'publica-' + ipIndex">{{ip}}</td>
  
              <td>{{ red.dominioRed }}</td>
  
  
  
  
  
  
  
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