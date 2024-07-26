<template >
  <barra-navegacion></barra-navegacion>
  
  <v-dialog
          v-model="VentanaGrabar"
          persistent
          width="500"
> 
<v-alert
        shaped
      color="#FF0000"
      theme="dark"
      icon="mdi-alert"
      density="compact"
      elevation="4"
      border="top"
    >
    Debe ingresar un dato
<!-- Alerta de confirmación personalizada -->
    <div v-if="mostrarAlertaGrabar"  role="alert">
          <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Info:">
              <use xlink:href="#info-fill" />
          </svg>
          <div>
              <div class="row">
                 
        <div class="col  p-3 text-center ">
        <v-btn  prepend-icon="mdi-cancel" color="#FF0000" @click="cerrarGrabar">   <v-spacer></v-spacer> Cerrar</v-btn>
      </div>
      </div>
          </div>
      </div>
      
      <!--fin alerta confirmacion obtenerValores-->
  </v-alert>
  </v-dialog>
<div  class="shadow p-3  bg-light text-sm " align-center style="max-width: 1350px; " >
<v-alert
       shaped
      color="blue-grey"
     
     theme="dark"
     icon="mdi-domain"
     density="compact"
     elevation="4"
     border="top"
   >
    <b> Consumo:  </b> 

    Carga de consumo de pacientes
   </v-alert>
   <br>
 <spinner :visible="MostrarSpinner"></spinner>
 <div v-if="!MostrarSpinner">
   <div >
     
     
     <!--nueva prueba-->
     <div class="container-sm shadow p-3  bg-white" style="max-width: 1300px; ">
       
       <div class="row " >
       
       <div class="col-2" >
         <v-text-field @keyup.enter="handleEnter" ref="cantidadField" v-model="Numero" label="Ingrese numero" variant="underlined" block></v-text-field>
       </div>
       <div class="col-1 "> 
             <v-btn @click="VerDatosAfi()" color="primary" prepend-icon="mdi-magnify" block></v-btn>  
       </div>
       <div class="col-8" >
         <v-text-field  v-model="VerDatosText" label="Datos" variant="underlined" block></v-text-field>
       </div>
       
     </div>
     <div class="row" >
       <div class="col-2" >
         <v-text-field  v-model="NComprobante"   label="Nro Comprobante" variant="underlined" block></v-text-field>
       </div>
       
       


       <div class="col-4" >
   Selecciona un sector
   <select v-model="ValorCombo" class="form-select" id="Combo" >
     <option value="0">Seleccionar un sector...</option> 
     <option v-for="Combo in ListaCombos" :key="Combo.codigo"  :value="Combo.codigo">{{Combo.codigo}} -- {{Combo.nombre}}</option>
   </select>  
     
</div>
<div class="col-2" ></div>
<div class="col-4" >
  <!--
  <v-btn @click="AgregarMed()" color="primary" p prepend-icon="mdi-cloud-upload" block>Agregar medicamentos</v-btn>         
  -->
  <v-card
                @click="AgregarMed()" 
                class="mx-auto"
                elevation="10"
                prepend-icon="mdi-arrow-up-bold-box-outline" 
                color ="primary"
              >
                <template v-slot:title>
                  Agregar medicamentos
                </template>

                <v-card-text>
                  Carga de consumo de medicamentos
                </v-card-text>
              </v-card> 
</div>
<div class="col-5">


 </div>
   </div>
 


   
 

  
 
   </div>  
 </div> 
 <br>   
 
 <AlertaMensaje  :visible = "mostrarAlertaSucesoMensaje" :mensaje = "mensajeAlertaSuceso" color="#FF0000"/>

     
 <div class="shadow p-3  bg-light text-sm " style="max-width: 1350px; ">
    
<div class="row">

<ListarMed />      



</div>


       
       
 
     
<v-dialog
 v-model="dialog"
 persistent
 fullscreen
>
<v-card>
  <div class="content" > 
  <v-text-field v-model="searchQuery" label="Buscador" append-inner-icon="mdi-magnify" variant="underlined" size="small" ></v-text-field>
 </div>
<!--Empieza Buscador-->

<div class="containerScroll">
<div class="content" ref="scrollContainer"> 
    
<table class="table table-striped bg-white text-left">
        <thead>
          <tr>
            <th v-for="(header, index) in headers" :key="index">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in paginatedRows" :key="rowIndex">
            <td v-for="(header, colIndex) in headers" :key="colIndex">
              <v-chip class="d-flex  darken-1 sm"   elevation="1"   > 
              {{ row[header] }}
            </v-chip>
            </td>
            <td>
            <v-btn @click="sendRowData(row)" class="bg-primary" >+</v-btn>
          </td>
          </tr>
          
        </tbody>
      </table>


</div>
</div>

  
            
             <!--FIN-->                  

<!--
             <div class="containerScroll">
 <div class="content" ref="scrollContainer">
<div class="row mt-5">

<div class="col-md-4 shadow p-3" v-for="item in ListaFormularios" v-bind:key="item.nroRegistro"> 

 <div class="card mb-4 bg-primary shadow p-3">
   
   <div class="card-body"><v-icon start icon="mdi-arrow-right" ></v-icon>
  {{ item.nombre }} -  {{ item.presentacion }}   
   
     
       <div class="row" >
           <div class="col-6 text-left "><strong>$</strong> {{ item.precio }} </div>
           <div class="col-6 text-center ">
             <v-btn fab  @click="Mostrar(  item.codigo, item.nombre, item.precio)" color="primary" prepend-icon="mdi-open-in-new">Seleccionar</v-btn>
           </div>
       </div>
       


     
   </div>
  
 </div>

</div>

</div>
</div>

</div>
-->
<div class="content"> 
<div class="row " >
       <div class="col-2" >
         <v-text-field v-model="MediCodigo" label="Codigo" variant="underlined" block></v-text-field>
       </div>
       <div class="col-6" >
         <v-text-field v-model="MediNOmbre" label="MedPresentacion" variant="underlined" block></v-text-field>
       </div>
       <div class="col-2" >
         <v-text-field v-model="MediPrecio" label="MedPrecio" variant="underlined" block></v-text-field>
       </div>
       </div>
       </div>
       <div class="content"> 
<div class="row" >
           <div class="col-6 text-center ">
             
             <v-text-field  v-model="dosis" label="Dosis" variant="underlined" block></v-text-field>
           </div>
         
           <div class="col-1 text-center "> 
             <v-text-field  v-model="MedCantidad" label="Cantidad"  variant="underlined" block></v-text-field>
           </div>
           <div class="col-4 text-center "> 
            <AlertaMensaje  :visible = "mostrarAlertaSucesoMensaje" :mensaje = "mensajeAlertaSuceso" color="#FF0000"/>
           </div>
           
         </div>
         </div>
<!--Termina Buscador-->
<v-card-actions>
         <v-spacer></v-spacer>
         
         <v-btn
           color="blue-darken-1"
           variant="text"
           @click="Grabar()"
           
         >
           Grabar Medicamento
         </v-btn>
         <v-btn
           color="blue-darken-1"
           variant="text"
           @click="cerrarventana()"
           prepend-icon="mdi-close" 
         >
           Cerrar
         </v-btn>
       
       </v-card-actions>
</v-card>

</v-dialog>

 
<!-- Nueva tabla-->
<!-- Caja de texto y boton para buscar -->
<!-- Botonoes y caja de texto para buscar -->



</div>


</div>

</div>
</template>
<script>

//import datos from "../assets/json/pokemones.json";
import ejemplo from '../components/ejemplo.vue';
import BarraNavegacion from '@/components/BarraNavegacion.vue';
import Spinner from '@/components/Spinner.vue';
import AlertaSuceso from '@/components/AlertaSuceso.vue';
import AlertaMensaje from '@/components/AlertaMensaje.vue';
import EditarFilaModal from '../components/EditarFilaModalN.vue';
import DataTable from 'datatables.net-vue3'
import Select from 'datatables.net-select';
import DataTablesCore from 'datatables.net-bs5';
import Buttons from 'datatables.net-buttons-bs5';
import 'datatables.net-responsive-bs5';
import ListarMed from '../components/ListarMed.vue';



import { ref } from 'vue';
import EditarFilaModalN from '../components/EditarFilaModalN.vue';

DataTable.use(DataTablesCore);
DataTable.use(DataTablesCore);
DataTable.use(Select);

const table = ref();
export default {
props:[],
     selected: [],
arreglobuscador: [],
name: 'TableCom',
name: "Formularios",
components: {
 'spinner': Spinner,
 'barra-navegacion': BarraNavegacion,
 EditarFilaModalN,
 ejemplo,
 ListarMed,
 AlertaMensaje,
 'alerta-suceso': AlertaSuceso,
  DataTable
},


data: function () {
 return {
 //-----------------------------
 //-----------------------------
 searchQuery: '',
   currentPage: 1,
   itemsPerPage: 5,
   VerDatosText: '',
   ValorCombo: '',
   ValorCombo1: '',
   mensajeAlertaSuceso: "",//mensaje alerta de suceso vacio
   VentanaGrabar: false,
   docentes: [], // <-- La lista de docentes
   ListObraSocial:[],
   codigo:'',
   nombre:'',
   valor:'',
   buscar: '',
   MediCodigo: '',
   MediNOmbre: '',
   MediPrecio: '',
   arreglobuscador: [],
   dialog: false,  
   selectedId: -1,
   selectedRow: '',
   lengthRules: [
   value => {
       if (  /[0-9-]+/.test(value) && value?.length > 5) return true
         return 'Acepta valores numericos y mas de 5 digitos.'
     },
   ],
    //************ */
     

   titulo_Modal:"",
   Id: null, 
   datos: null,
   ListaCombos: null,
   ListaCombosOrigen: null,
   ListaFormularios: null,
   MostrarSpinner: false,
   NoHayRegistros: false,
   mostrarAlertaEliminar: false,
   mostrarAlertaSuceso: false,
   mostrarAlertaSucesoMensaje: false,
   mensajeAlertaSuceso:"",
   idConfigFormToDelete: null,
   Fecha:"",
   MedCantidad:"",
   ValorComboOrigen:"",
   Entrega:0,
   
 }
},
created() {

 //this.fetch();
 this.SelectedObraSocial();
 this.MostrarCombo();
 this.MostrarComboOrigen();
 //alert("hola");
 this.ValorCombo = "0";
 this.idUsuario = this.$store.state.id_usuario;
 this.BuscarMedicamento();
 this.fetchArticulosMed();
 
 
},
computed: {
        
//--------------------------
//--------------------------
headers() {
        return this.rows.length > 0 ? Object.keys(this.rows[0]) : [];
      },
filteredRows() {
        if (!this.searchQuery) {
          return this.rows;
        }
        const query = this.searchQuery.toLowerCase();
        return this.rows.filter(row => 
          Object.values(row).some(value => 
            String(value).toLowerCase().includes(query)
          )
        );
      },
     
      paginatedRows() {
        const start = (this.currentPage - 1) * this.itemsPerPage;
        const end = start + this.itemsPerPage;
        return this.filteredRows.slice(start, end);
      },
      totalPages() {
        return Math.ceil(this.filteredRows.length / this.itemsPerPage);
      },

//--------------------------
//--------------------------
         formTitle () {
            return this.Entrega  === 0 ? 'Gargar nuevos datos' : 'Modificar datos'
         },
     //*********************** */
         ListaFormularios1() {              
           return this.datos && this.datos.filter(item => {
           return item.nombre.toLowerCase().includes(this.buscar.toLowerCase());  
         });
         },
         //********************* */

       



         //******************* */
      
     },
methods: {
//--------------------------
//--------------------------

nextPage() {
   if (this.currentPage < this.totalPages) {
     this.currentPage++;
   }
 },
 prevPage() {
   if (this.currentPage > 1) {
     this.currentPage--;
   }
 },
//--------------------------
//--------------------------
 
 onSelect(e, dt, type, indexes ){
   //var rowData = dt.rows( indexes ).data().toArray();
   this.string_id = indexes;
   this.dialog = true;
   console.log("aca estoy")
       console.log(dt);
     },
     sendRowData(row) {
      const keys = Object.keys(row);
      //alert(keys[0]); Nombre de la columna
      const entries = Object.entries(row);
      const primerpar = entries[1];  // Valor de la columna
      const nombre = entries[2];  // Valor de la columna
      const precio = entries[3];  // Valor de la columna
      //alert('Dato de la fila seleccionada:', row);
      console.log('Dato de la fila seleccionada:', primerpar[1]);
      //this.processRow(row);
      this.MediCodigo = primerpar[1];
      this.MediNOmbre =nombre[1];
      this.MediPrecio = precio[1];
      
    },
     Mostrar(V1, V2, V3){
     
       this.MediCodigo = V1;
       this.MediNOmbre =V2;
       this.MediPrecio = V3;
       
     },
 limpiar(){
   this.string_id = "";
   this.default_value ="";
   this.value_list ="";
 },
 async fetchArticulosMed() {
        
        //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud 
        //const respuesta = await this.axios.get("/api/ConfigForm/ListaField?pTipo=2136")
        const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idUsuario}`)
          .then((respuesta) => {
            //this.ListaFormulariosArticulos = respuesta.data.lista
            this.rows = respuesta.data.lista;
            console.log("IMPORTANTE Muestro rows ADRIAN")
            console.table(this.rows);     
          })
          .catch(err => {
            //console.log(err);
          });
      // this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
      },
 nuevo(){
   this.Entrega = 0;
   this.dialog = true;
   this.string_id = "";
   this.default_value ="";
   this.value_list ="";
 },
 cerrarventana(){
   this.dialog = false;
   
 },
 cerrarGrabar() {
          this.VentanaGrabar = false;
      },
 AgregarMed(){
  if (!this.Numero || this.Numero.length == 0) {
    this.$refs.cantidadField.$el.querySelector('input').focus();
        this.mostrarAlertaEliminar = false;
        this.mostrarAlertaSucesoMensaje = true;
        this.mensajeAlertaSuceso = "Debe Ingresar un numero internacion";
        setTimeout(() => {
        this.mostrarAlertaSucesoMensaje = false;
        }, 5000);
        return;
   }
     //this.ListaFormularios = null;
     this.dialog = true;
     this.MediCodigo = "";
     this.MediNOmbre = "";
     this.MediPrecio = "";
   },
 editar(Listaform){
   
   this.Entrega = 1;
   this.dialog = true;
   this.string_id = Listaform.string_id;
   this.default_value = Listaform.default_value;
   this.value_list = Listaform.value_list;
   this.mask_library = Listaform.mask_library;
   this.assumed_value = Listaform.assumed_value;
   this.length = Listaform.length;
 },
 VerDatosAfi(){
   
   this.VerDatosText = "Riveros Hugo Adrian - Obra Social: Medife - Plan: Bronce";
  
 },
 handleEnter() {
   // Este método se activará cuando se presione la tecla "Enter"
   if (this.Numero) {
   this.VerDatosText = "Riveros Hugo Adrian - Obra Social: Medife - 430101: Pension en cama con dos baños privados";
   //this.ValorCombo = "2";
   //this.ValorComboOrigen = "2258";
   //this.selectedItem = "Elemento2";
 } else {
     alert('Por favor ingresa un número antes de presionar "Enter"');
   }
   // Aquí puedes agregar la lógica que deseas ejecutar cuando se presione "Enter"
 },
 verId(){
   alert("Hola")
 },
 async BuscarMedicamento() {
  
  //if (!this.buscar || this.buscar.length == 0) {

//this.mostrarAlertaEliminar = false;
//this.mostrarAlertaSucesoMensaje = true;
//this.mensajeAlertaSuceso = "Debe Ingresar un nombre de medicamento";
//setTimeout(() => {
//this.mostrarAlertaSucesoMensaje = false;
//}, 5000);
//return;
//}
//alert("medciamento");
   //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
   const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idUsuario}`)
   //const respuesta = await this.axios.get(`/api/ConfigForm/BuscarArticulos?pTipo=${this.idUsuario}&pNombre=${this.buscar}`, {
 //timeout: 100000 // Tiempo de espera en milisegundos (10 segundos en este caso)


 
//})
     .then((respuesta) => {
       this.ListaFormularios = respuesta.data.lista
       this.rows = respuesta.data.lista;
       
       console.log("Importante Lista Medicamentos");
       console.table(this.ListaFormularios);
       this.datos = this.ListaFormularios;
       //console.log("Importante Lista Datos");
       //console.table(this.datos);
      
       //si no hay formularios en la respuesta de la api mostrar mensaje
       if (this.ListaFormularios.length == 0) {
         //this.NoHayRegistros = true
         alert("No se encontraron datos para la busqueda")
       }
     })
     .catch(err => {
       console.log(err);
     });
     
         
   //this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
 },
 async MostrarCombo() {
   
   this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
   const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=4&pId=0")
     .then((respuesta) => {
       this.ListaCombos = respuesta.data.lista;
       
       console.log("Lista Combos");
       console.log(this.ListaCombos);
      
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
 async MostrarComboOrigen() {
   
   this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
   const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2135")
     .then((respuesta) => {
       this.ListaCombosOrigen = respuesta.data.lista;
       
       console.log("Lista ListaCombosOrigen");
       console.log(this.ListaCombosOrigen);
      
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
 async SelectedObraSocial(){
           let me=this;
          
           var empresasArray=[];
           const respuesta = await this.axios.get("/api/ConfigForm/ListaRespuestas/2129")
           .then((respuesta) => {
             empresasArray=respuesta.data.lista;
             console.log (empresasArray);
             empresasArray.map(function(x){
                 //me.ListObraSocial.push({text: x.valor,value:x.valor})
                 me.ListObraSocial.push({text: x.valor})
                 }); 
                 console.log("Muestro Combo");  
                 console.log (me.ListObraSocial);
           }).catch(function(error){
               console.log (error);
           });
 },
 mostrarConfirmacionEliminar(Entrega) {
   this.mostrarAlertaEliminar = true;
this.idConfigFormToDelete = this.string_id; // Guarda el idConfigForm en data

 },
 cancelarEliminacion() {
   this.mostrarAlertaEliminar = false;
 },
 cerrarventana(){
     this.dialog = false;
     
   },
 async Agregar() {
   if(this.Entrega == 1)//Modifica
     this.Modificar();//alert("Modiifca Campo");
     else
     this.Grabar();//alert("Agrega Campo");
 },
 async fetch() {
         //alert("hola");
         this.MostrarSpinner = true;
         const idFormulario = this.$route.params.idConfigForm;
         this.idConfigForm = idFormulario;
         await this.axios.get(`/api/ConfigForm/ListaRespuestas/2134`)
         //await this.axios.get(`/api/ConfigForm/ListarMedicamentosClinicas?pIdClinica=${idFormulario}`)
             .then((respuesta) => {
                 let data = []; //declarar la variable data
                 data = respuesta.data.lista; //signarle a data el array de objetos recibidos de la api
                 this.ListaFormularios = respuesta.data.lista
                 this.datos = this.ListaFormularios;
                
                 //this.datos = this.data
                 console.log("tabla");
                 console.log (this.datos);
                 
                 if (data.length === 0) {
                     this.NoHayRegistros = true;}

                 // Objeto para almacenar los encabezados de columna
                 const columnHeaders = {};
                 // Objeto para almacenar las filas de la matriz
                 const matrix = {};
                 //console.log(data);
                 // Itera sobre los objetos
                 data.forEach(item => {
                     const rowId = item.identificador_fila;  // Usa el identificador_fila como identificador de fila
                     const columnId = item.id_Field; // Usa el id_Field como identificador de columna
                     const columnName = item.nombre; // Usa el nombre como encabezado de columna
                     const columnValue = item.valor; // Valor que se colocará en la matriz
                     const idDeValor = item.id_Answer; //identificador del valor que servira para poder editar un valor especifico
                     const Titulo = item.titulo; //titulo
                     // Agrega el nombre de columna a los encabezados
                     columnHeaders[columnId] = columnName;

                     // Crea una fila si no existe
                     if (!matrix[rowId]) {
                         matrix[rowId] = {};
                     }
                     
                     // Asigna el valor a la columna correspondiente en la fila
                     matrix[rowId][columnName] = columnValue;

                     // Agrega también el identificador de fila
                     matrix[rowId]['identificador_fila'] = rowId;
                     matrix[rowId][`${columnName}_id_Field`] = item.id_Field;
                     matrix[rowId][`${columnName}_id_Answer`] = item.id_Answer;
                     matrix[rowId][`${columnName}_id_ConfigForm`] = item.id_ConfigForm;
                     matrix[rowId][`${columnName}_titulo`] = item.titulo;
                     

                 });
                 

                 //iteracion de los encabezados
                 const headers = [...new Set(data.map(item => item.nombre))];

                 const matrixArray = Object.values(matrix).map(row => {
                     const rowWithIds = [row.identificador_fila];

                     headers.forEach(header => {
                         const cellData = {
                             id_ConfigForm: row[`${header}_id_ConfigForm`],
                             id_Field: row[`${header}_id_Field`],
                             id_Answer: row[`${header}_id_Answer`],
                             value: row[header] || null
                         };

                         rowWithIds.push(cellData);
                     });

                     return rowWithIds;
                 });
                 
                 this.dataHeaders = headers;  //Encabezados de columna
                 console.log("headers");
                 console.log(this.dataHeaders);
                 this.dataValues = matrixArray;  //Matriz de datos
                 console.log("tabla con datos a buscar");
                 //this.datos = matrixArray;
                 console.log(this.dataValues);
                
                 
                 

             })
             .catch(err => {
                 console.log(err);
             });
             //Codigo Nuevo

             const idConfigForm = this.$route.params.idConfigForm;
         this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/2134`)
             .then((respuesta) => {
             this.daform = respuesta.data;
             //this.dafield = respuesta.data.datosField;
             //console.log("valor de la tabla");
             //console.log(this.daform);
             })
             .catch(err => {
             console.log(err);
             }).finally(() => {
             //finaliza el spinner
             // Ocultamos el spinner luego de finalizar la solicitud
             this.MostrarSpinner = false;
             });
             //Fin Codigo Nuevo
             this.MostrarSpinner = false;
     },
     //Buscador Uno buscaruno
     async buscador() {
        
         const valor = this.buscaruno;
         this.MostrarSpinner = true;
         const idFormulario = this.$route.params.idConfigForm;
         this.idConfigForm = idFormulario;
         await this.axios.get(`/api/ConfigForm/Buscar/${idFormulario}/${valor}`)
         //await this.axios.get(`/api/ConfigForm/Buscar?pIdClinica=${idFormulario}`)
             .then((respuesta) => {
                 let data = []; //declarar la variable data
                 data = respuesta.data.lista; //signarle a data el array de objetos recibidos de la api
                 this.ListaFormularios = respuesta.data.lista
                 this.datos = this.ListaFormularios;
                 //this.datos = this.data
                 console.log("tabla Buscador");
                 console.log (this.datos);
                 
                 if (data.length === 0) {
                     this.NoHayRegistros = true;}

                 // Objeto para almacenar los encabezados de columna
                 const columnHeaders = {};
                 // Objeto para almacenar las filas de la matriz
                 const matrix = {};
                 //console.log(data);
                 // Itera sobre los objetos
                 data.forEach(item => {
                     const rowId = item.identificador_fila;  // Usa el identificador_fila como identificador de fila
                     const columnId = item.id_Field; // Usa el id_Field como identificador de columna
                     const columnName = item.nombre; // Usa el nombre como encabezado de columna
                     const columnValue = item.valor; // Valor que se colocará en la matriz
                     const idDeValor = item.id_Answer; //identificador del valor que servira para poder editar un valor especifico
                     const Titulo = item.titulo; //titulo
                     // Agrega el nombre de columna a los encabezados
                     columnHeaders[columnId] = columnName;

                     // Crea una fila si no existe
                     if (!matrix[rowId]) {
                         matrix[rowId] = {};
                     }
                     
                     // Asigna el valor a la columna correspondiente en la fila
                     matrix[rowId][columnName] = columnValue;

                     // Agrega también el identificador de fila
                     matrix[rowId]['identificador_fila'] = rowId;
                     matrix[rowId][`${columnName}_id_Field`] = item.id_Field;
                     matrix[rowId][`${columnName}_id_Answer`] = item.id_Answer;
                     matrix[rowId][`${columnName}_id_ConfigForm`] = item.id_ConfigForm;
                     matrix[rowId][`${columnName}_titulo`] = item.titulo;
                     

                 });
                 

                 //iteracion de los encabezados
                 const headers = [...new Set(data.map(item => item.nombre))];

                 const matrixArray = Object.values(matrix).map(row => {
                     const rowWithIds = [row.identificador_fila];

                     headers.forEach(header => {
                         const cellData = {
                             id_ConfigForm: row[`${header}_id_ConfigForm`],
                             id_Field: row[`${header}_id_Field`],
                             id_Answer: row[`${header}_id_Answer`],
                             value: row[header] || null
                         };

                         rowWithIds.push(cellData);
                     });

                     return rowWithIds;
                 });
                 
                 this.dataHeaders = headers;  //Encabezados de columna
                 console.log("headers");
                 console.log(this.dataHeaders);
                 this.dataValues = matrixArray;  //Matriz de datos
                 console.log("tabla con datos a buscar");
                 //this.datos = matrixArray;
                 console.log(this.dataValues);
                 
                 

             })
             .catch(err => {
                 console.log(err);
             });
             //Codigo Nuevo

             const idConfigForm = this.$route.params.idConfigForm;
         this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/2134`)
             .then((respuesta) => {
             this.daform = respuesta.data;
             
             })
             .catch(err => {
             console.log(err);
             }).finally(() => {
             //finaliza el spinner
             // Ocultamos el spinner luego de finalizar la solicitud
             this.MostrarSpinner = false;
             });
             //Fin Codigo Nuevo
             this.MostrarSpinner = false;
     },
 async Grabar() {
  if (!this.MediCodigo || this.MediCodigo.length == 0) {
    
this.mostrarAlertaEliminar = false;
this.mostrarAlertaSucesoMensaje = true;
this.mensajeAlertaSuceso = "Debe Ingresar un medicamento";
setTimeout(() => {
this.mostrarAlertaSucesoMensaje = false;
}, 5000);
return;
}
if (!this.dosis || this.dosis.length == 0) {

this.mostrarAlertaEliminar = false;
this.mostrarAlertaSucesoMensaje = true;
this.mensajeAlertaSuceso = "Debe Ingresar dosis";
setTimeout(() => {
this.mostrarAlertaSucesoMensaje = false;
}, 5000);
return;
}
if (!this.MedCantidad || this.MedCantidad.length == 0) {

this.mostrarAlertaEliminar = false;
this.mostrarAlertaSucesoMensaje = true;
this.mensajeAlertaSuceso = "Debe Ingresar una cantidad";
setTimeout(() => {
this.mostrarAlertaSucesoMensaje = false;
}, 5000);
return;
}
  
     
     await this.axios.post(`/api/ConfigForm/AgregarConsumo/${this.Numero}/${this.MediCodigo}/${this.NComprobante}/123/${this.dosis}/24%2F07%2F2024/${this.VerDatosText}/${this.MedCantidad}/${this.ValorCombo}/42`)
     .then(datos => {
       this.mostrarAlertaEliminar = false;
       this.mensajeAlertaSuceso = "Grabaron Correctamente los datos";
       this.mostrarAlertaSuceso = true;
      alert("Segrabaron los datos");

       setTimeout(() => {
                this.mostrarAlertaSuceso = false;
             }, 5000);
     });
     window.location.reload();
 },
 async Modificar() {
   
     await this.axios.put(`/api/ConfigForm/ModificaCampos/1/${this.string_id}/${this.default_value}/${this.value_list}/${this.mask_library}/${this.assumed_value}/${this.length}`)
     .then(datos => {
       this.mostrarAlertaEliminar = false;
       this.mensajeAlertaSuceso = "Los datos se modificaron correctamente";
       this.mostrarAlertaSuceso = true;
     

       setTimeout(() => {
                this.mostrarAlertaSuceso = false;
             }, 5000);
     });
 },
 async eliminarform(idConfigFormToDelete) {
   await this.axios.put(`/api/ConfigForm/EliminaCampos/1/${this.idConfigFormToDelete}`)
   //await this.axios.put(`/api/ConfigForm/EliminaCampos/1/1`)
     .then(datos => {
       this.mostrarAlertaEliminar = false;
       this.mensajeAlertaSuceso = "Eliminado exitosamente";
       this.mostrarAlertaSuceso = true;
     
       window.location.reload();
       setTimeout(() => {
                this.mostrarAlertaSuceso = false;
             }, 5000);
     });
 },

},
}
</script>
<style>
@import 'datatables.net-dt';
.custom-margin-botonN{
margin-left: 115px; /* Ajusta el valor según tus necesidades */
}
.table-container {
max-height: 420px; /* ajusta la altura máxima según tus necesidades */
overflow-y: auto;
}
tr.v-data-table__selected {
background: #7d92f5 !important;
}
.containerScroll {
width: 100%; /* Ancho del contenedor */
height: 500px; /* Altura fija del contenedor */

overflow-y: auto; /* Habilita el desplazamiento vertical cuando el contenido excede la altura */
}
.content {
padding: 10px; /* Espacio interno */
}
.pagination {
display: flex;
justify-content: center;
align-items: center;
margin-top: 10px;
}

.pagination button {
margin: 0 5px;
padding: 5px 10px;
}
</style>