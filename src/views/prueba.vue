<template >
  <v-card  class="px-4 py-2  text-center w-100 bg-light" elevation="3"  style="max-width: 1200px; ">
    <div class="row bg-white" >
  <div class="col-3" >
  <v-text-field v-model="codigo" label="codigo"  variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-6" >
  <v-text-field v-model="nombre" label="nombre"  variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-3" >
  <v-btn @click="ver()" class="bg-primary" p prepend-icon="mdi-cloud-upload" block>Ver Datos</v-btn> 
</div>
</div>
 <!-- Listado de datos cargados -->
    <combobox />
   </v-card>
</template>
<script>


import combobox from '../components/combobox.vue';





//import { computed , onMounted, ref } from "vue";



export default {

  components: {

    combobox
  },
  
  props: {
    msg: String
  },
  
  data: function () {
    return {
    
      codigo: '',
      nombre: '', 
    
      
      
    }
  },
  created() {
    

    
  },
  computed: {

         
        },
  methods: {
  
    ver(){
      console.log(this.codigo); // Aquí se obtiene el valor del campo 'codigo'
      console.log(this.nombre); // Aquí se obtiene el valor del campo 'nombre'
    },
    async fetch() {
      
      this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCamposString?pTipo=1")
        .then((respuesta) => {
          this.ListaFormularios = respuesta.data.lista
          this.datos = this.ListaFormularios;
          console.log("Importante");
          console.table(this.datos);
         
          //si no hay formularios en la respuesta de la api mostrar mensaje
          if (this.ListaFormularios.length == 0) {
            this.NoHayRegistros = true
          }
        })
        .catch(err => {
          console.log(err);
        });
        
            
      this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
    },
    
 
   
  
    
 
  
   
  },
}
</script>
<style>


</style>