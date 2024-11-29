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
                <input v-model="formData.numeroFicha" type="text" class="form-control border border-dark" aria-label="Username"
                    aria-describedby="addon-wrapping">
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
                <input v-model="formData.serial"  type="text" class="form-control border border-dark" aria-label="Username"
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

      
  
    <section class="register">

      
      <h3>Registros</h3>
    <ul>
      <li v-for="(equipo, index) in registros" :key="index">
        <span>
          {{ equipo.numeroFicha }} -
          {{ equipo.fecha }} -
          {{ equipo.codigoInventario }} -
          {{ equipo.marca }} -
          {{ equipo.modelo }} -
          {{ equipo.serial }} -
          {{ equipo.funcion }}
        </span>
        <button @click="editar(index)">Editar</button>
        <button @click="eliminar(index)">Eliminar</button>
      </li>
    </ul>

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


<style>

.datos_equipo{
    display: block;
    border-radius: 10px;
    border: 1px solid black;
    width: 50%;
    padding-bottom: 2%;
    margin-left: 1%;
    
}


.title_equipo{
    margin-left: 3%;
    font-size: 18px;
    font-style: bold;
    margin-top: 8%;
    margin-bottom: -1.3%;
}

.cod_inv{
    width: 30%;
    margin-left: 30%;
    margin-top: -2%;
}

.fcha{
    width: 70%;
    margin-left: 130%;
    margin-top: -30%;
}

.input-group{
    margin-top: 1%;
}

.datos{
    width: 320%;
    margin-top: 20%;
    margin-left: -93%;
}

.func_equipo{
    margin-top: 1%;
    width: 320%;
    margin-left: -93%;
}

.btn-success{
  margin-top: 4%;
  margin-left: 91.5%;
}

.register{
  border: 2px solid black;
  border-radius: 10px;
  border: 1px solid black;
  width: 40%;
  padding-bottom: 2%;
  margin-left: 56%;
  margin-top: -19.4%;
}

.register h3{
  margin: 5%;
}





</style>