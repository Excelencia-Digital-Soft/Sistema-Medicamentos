<template>
  <v-chip class="d-flex  darken-1 sm"  color="#000000" elevation="1"   >Buscador de Medicamentos en AlfaBeta</v-chip>

<div class="content">  
     <div class="row shadow p-3" >
            <div class="col-9 text-center ">
              
              <v-text-field  v-model="buscar" label="Busqueda por nombre de medicamento de AlfaBeta" variant="underlined" block></v-text-field>
            </div>
            <div class="col-3 text-center "> 
              <v-btn @click="BuscarMedicamento()" class="bg-primary" p prepend-icon="mdi-cloud-upload" block>Buscar en AlfaBeta</v-btn> 
            </div>
            
          </div>
</div>
<div >
  <div class="content" ref="scrollContainer">
    <div class="row mt-5">
      <div class="col-md-4" v-for="item in ListaFormulariosMed" v-bind:key="item.nroRegistro"> 
        <div class="card mb-4 ">
          <div class="card-body"><v-icon start icon="mdi-arrow-right" ></v-icon>
            {{ item.nombre }} -  {{ item.presentacion }}     
              <div class="row" >
                <div class="col-6 text-left "><strong>$</strong> {{ item.precio }} </div>
                <div class="col-6 text-center ">
                <v-btn class="bg-primary" fab  @click="Mostrar(  item.nombre, item.precio, item.nroRegistro, item.presentacion)"  prepend-icon="mdi-open-in-new">Seleccionar</v-btn>
                </div>
          </div>        
       </div>
       </div>
     </div>

</div>
</div>

</div>


</template>
<script>
import AlertaSuceso from "../components/AlertaSuceso.vue";
export default {
name: 'EditarFilaModalN',
components: {
  AlertaSuceso,
},
props: {
  fila: Object,
  campoTexto: String,
},
data() {
  return {
          buscar: '',
          ListaFormulariosMed: null,
      };
  },
  computed: {
  },
  mounted() {
  },
  created() {
     

  },
 methods: {
  Mostrar(V1, V2, V3, V4) {
  
    const inputDetalleInternado = document.getElementsByName("nroregistro")[0];
      inputDetalleInternado.value = V3;
      const pPrecio = document.getElementsByName("precio")[0];
      pPrecio.value = V2;
      const pNombre = document.getElementsByName("nombre")[0];
      pNombre.value = V1 +" -  "+ V4;
      this.ListaFormulariosMed = null;
    
  },
  async BuscarMedicamento() {
  const respuesta = await this.axios.get(`/api/ConfigForm/BuscaAlfaBetaNombre?pNombre=${this.buscar}`, {
  
})
      .then((respuesta) => {
      this.ListaFormulariosMed = respuesta.data.lista
      this.datosMed = this.ListaFormulariosMed;
      if (this.ListaFormulariosMed.length == 0) {
          //this.NoHayRegistros = true
          alert("No se encontraron datos para la busqueda")
        }
      })
      .catch(err => {
        console.log(err);
      });
  },
},

}
</script>