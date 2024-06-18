<template>
<v-chip class="d-flex  darken-1 sm"   elevation="1"   > 
    Listar en Medicamentos 

</v-chip>
    <!-- Tabla que muestra los medicamentos-->

<div style="max-width: 1300px" class="shadow p-3 mb-2 bg-white rounded table-container text-sm container-sm" v-if="$store.state.permisos.includes(11) & !NoHayRegistros">
          <!-- Tabla del Formulario -->
           <div class="row" >
              <div class="col  p-3 text-center ">
               
                </div>
                <div class="col  p-3 text-center ">
                 
                </div>
                <div class="col  p-3 text-center ">
                  <v-text-field v-model="buscar" label="Buscador por nombre de medicamento" append-inner-icon="mdi-magnify" variant="underlined" size="small" ></v-text-field>
                </div>
          </div>  
     
<table :value="customers" class="table  table-hover "  color="#000000" >
          <thead>
            <tr>
              <th ><v-chip class="justify-center " color="#000000">Identificador</v-chip></th>
              <th ><v-chip class="justify-center "  color="#000000">Codigo</v-chip></th>
              <th ><v-chip class="justify-center "  color="#000000">Nombre</v-chip></th>
              <th ><v-chip class="justify-center "  color="#000000">Precio</v-chip></th>
              <th ><v-chip class="justify-center "  color="#000000">Nro Registro</v-chip></th>
              <th  ><v-chip class="justify-center"  color="#000000">Ver Datos</v-chip></th>
            </tr>
          </thead>
          <tbody v-for="ListaMed of ListaFormulariosArticulos" :key="ListaMed.articulosid">
            <tr>
              <td class="bg-white " >
                
                  <v-icon start icon="mdi-arrow-right" ></v-icon>  {{ ListaMed.articulosid }}
             
            </td>
              <td class="bg-white ">
    
              {{ ListaMed.codigo }}
           
              </td>
              <td  class="bg-white ">{{ ListaMed.nombre }}</td>
              <td  class="bg-white ">$ {{ ListaMed.precio }}</td>
              <td  class="bg-white ">{{ ListaMed.nroregistro }}</td>
              <td class="nowrap bg-white " >
                <div class="row">
                  <div class="col-auto">
                     <v-btn @click="VerArticulos(ListaMed)"  prepend-icon="mdi-open-in-new" class="sm"></v-btn>
                  </div>
                
                </div>
              </td>
            </tr>
         
         
          </tbody>
       
          
        </table> 

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
            idUsuario: null,
            ListaFormulariosArticulos: null,
            datosArticulos: null,
        };
    },
    computed: {
        ListaFormulariosArticulos() {
        //alert("Ingreso a Filter");
        //const idFormulario = this.$route.params.idConfigForm;
        //if(idFormulario == 2136){
          if (!this.datosArticulos) {
        return [];
      }
          return this.datosArticulos.filter(item => {
          return item.nombre.toLowerCase().includes(this.buscar.toLowerCase());
        });
            },
    },
    mounted() {
    },
    created() {
        this.idUsuario = this.$store.state.id_usuario;
        this.fetchArticulosMed();
        

    },
   methods: {
    VerArticulos(Listaform){
        //alert(Listaform.codigo);
        const inputCodigo = document.getElementsByName("Codigo")[0];
        inputCodigo.value = Listaform.codigo;
        const inputNroRegistro = document.getElementsByName("NroRegistro")[0];
        inputNroRegistro.value = Listaform.nroregistro;
        const pPrecio = document.getElementsByName("Precio")[0];
        pPrecio.value = Listaform.precio;
        const pNombre = document.getElementsByName("Nombre")[0];
        pNombre.value = Listaform.nombre;
        //this.ListaFormulariosMed = null;
      },
    async fetchArticulosMed() {
        
        //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud 
        const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idUsuario}`)
          .then((respuesta) => {
            this.ListaFormulariosArticulos = respuesta.data.lista
            this.datosArticulos = this.ListaFormulariosArticulos;
            console.log("IMPORTANTE Muestro ListaFormulariosArticulos")
            console.table(this.ListaFormulariosArticulos);     
          })
          .catch(err => {
            //console.log(err);
          });
      // this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
      },
    
},

}

</script>