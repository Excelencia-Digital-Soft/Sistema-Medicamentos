<template >
 -----------------------------------------------------------------------------------------------<br>
    -----------------Aca Componente-------------------------------------------------------------<br>
    -----------------------------------------------------------------------------------------------<br>
    <div class="container-sm shadow p-3" >
    <ejemplo />
  </div>
    <spinner :visible="MostrarSpinner"></spinner>
    <div v-if="!MostrarSpinner">
      <div >
        
        
        <!--nueva prueba-->
        <div class="container-sm shadow p-3" >
        <div class="row " >
          <div class="col-3" >
            <v-text-field @keyup.enter="handleEnter" v-model="Numero" label="Ingrese numero" variant="underlined" block></v-text-field>
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
            <v-text-field  v-model="Fecha" type="date" label="Fecha" variant="underlined" block></v-text-field>
          </div>
          <div class="col-5" >
      Selecciona un sector
      <select v-model="ValorCombo" class="form-select" id="Combo" >
        <option value="">Seleccionar un sector...</option> 
        <option v-for="Combo in ListaCombos" :key="Combo.codigo"  :value="Combo.codigo">{{Combo.codigo}} -- {{Combo.nombre}}</option>
      </select>  
        <h5>Valor del Combo Codigo: {{ListaCombos.codigo}}--{{ValorCombo.nombre}} </h5>
</div>
<div class="col-5">
    Selecciona un origen      
    <select v-model="ValorComboOrigen" class="form-select" >  
      <option value="">Seleccionar un origen...</option> 
      <option v-for="ComboO in ListaCombosOrigen" :key="ComboO.codigo"  :value="ComboO.codigo">{{ComboO.nombre}}</option>
    </select>
 
    </div>
      </div>
      <div class="row" >
      <div class="col-4"></div>
      <div class="col-4"></div>
      <div class="col-4">
        <v-btn @click="AgregarMed()" color="primary" p prepend-icon="mdi-cloud-upload" block>Agregar medicamentos</v-btn> 
      </div>
    </div>
  
   
      
    

     
    
      </div>  
    </div>    
        
          <!-- <datatables :data="ListaFormularios" class="table" style="width:80%">
            <thead>
          <tr>
            <th >ID</th>
            <th >Titulo del formulario</th>
            <th >Descripcion</th>
            <th  >Acciones</th>
          </tr>
        </thead>
          </datatables> --> 
          <!-- Iconos
          https://vuetifyjs.com/en/components/icons/#semantic-svg-icons

          <v-icon icon="mdi-home" />
          <v-icon icon="mdi-arrow-left" />
          <v-icon icon="mdi-arrow-right" />
          <v-icon icon="mmdi-wrench" />
          <v-icon icon="mdi-thumb-up" />
          <v-icon icon="mdi-minus-circle" />
          <v-icon end icon="mdi-cancel"></v-icon>
          <v-icon end icon="mdi-checkbox-marked-circle"></v-icon>
          <v-icon size="large" color="green-darken-2" icon="mdi-domain" ></v-icon>
          <v-icon size="large" color="orange-darken-2" icon="mdi-arrow-up-bold-box-outline" ></v-icon>
          
          -->

         <p></p> <p></p>    
        
    <div class="container-sm">
       
<div class="row">
 
        
 


</div>

        


       
        

 
     aca estoy   
        
{{ ListaCombos }} 
          
          
       <!--  {{ ListaFormularios }}   -->
         
       
 
 <!-- @select="editar(ListaFormularios)" 
      
<DataTable 
          
          
          :data="ListaFormularios" 
          :columns="columns" 
          ref="tableCom"
           class="Dysplay"
           
           @select="verId(ListaFormularios)"
          
           :options="{
          
          select:{
                style: 'multi',
                selector: 'td:first-child'
            },
            
            select:true,
            responsive: true,
            autoWidth:false,
            lengthMenu: [5,20,50],
            columnDefs: [
            { orderable: false, targets: [3] },
            { width: '40%', targets: [1] },
            { width: '30%', targets: [3] },
            ],
            
            language: {
                processing: 'Procesando...',
                lengthMenu: 'Mostrar _MENU_ registros',
                zeroRecords: 'No se encontraron resultados',
                emptyTable: 'Ningún dato disponible en esta tabla',
                infoEmpty: 'Mostrando registros del 0 al 0 de un total de 0 registros',
                infoFiltered: '(filtrado de un total de _MAX_ registros)',
                search: 'Buscar:',
                infoThousands: ',',
                loadingRecords: 'Cargando...',
                paginate: {
                first: 'Primero',
                last: 'Último',
                next: 'Siguiente',
                previous: 'Anterior',
                },
                aria: {
                sortAscending: ': Activar para ordenar la columna de manera ascendente',
                sortDescending: ': Activar para ordenar la columna de manera descendente',
                },
                buttons: {
                copy: 'Copiar',
                colvis: 'Visibilidad',
                collection: 'Colección',
                colvisRestore: 'Restaurar visibilidad',
                copyKeys:
                    'Presione ctrl o u2318 + C para copiar los datos de la tabla al portapapeles del sistema. <br /> <br /> Para cancelar, haga clic en este mensaje o presione escape.',
                copySuccess: {
                    1: 'Copiada 1 fila al portapapeles',
                    _: 'Copiadas %ds fila al portapapeles',
                },
                copyTitle: 'Copiar al portapapeles',
                csv: 'CSV',
                excel: 'Excel',
                pageLength: {
                    '-1': 'Mostrar todas las filas',
                    _: 'Mostrar %d filas',
                },
                pdf: 'PDF',
                print: 'Imprimir',
                renameState: 'Cambiar nombre',
                updateState: 'Actualizar',
                createState: 'Crear Estado',
                removeAllStates: 'Remover Estados',
                removeState: 'Remover',
                savedStates: 'Estados Guardados',
                stateRestore: 'Estado %d',
                },
               
               
                searchBuilder: {
               
               
              
                data: 'Data',
                deleteTitle: 'Eliminar regla de filtrado',
                leftTitle: 'Criterios anulados',
                logicAnd: 'Y',
                logicOr: 'O',
                rightTitle: 'Criterios de sangría',
                title: {
                    0: 'Constructor de búsqueda',
                    _: 'Constructor de búsqueda (%d)',
                },
                value: 'Valor',
                },
                searchPanes: {
                clearMessage: 'Borrar todo',
                collapse: {
                    0: 'Paneles de búsqueda',
                    _: 'Paneles de búsqueda (%d)',
                },
                count: '{total}',
                countFiltered: '{shown} ({total})',
                emptyPanes: 'Sin paneles de búsqueda',
                loadMessage: 'Cargando paneles de búsqueda',
                title: 'Filtros Activos - %d',
                showMessage: 'Mostrar Todo',
                collapseMessage: 'Colapsar Todo',
                },
                
             
             
                info: 'Mostrando Registrss _START_ a _END_ de _TOTAL_ registros ',
               
            },

            }" >
            <thead>
                <tr>
            <th >troquel</th>
            <th >codBarras</th>
            <th >NroRegistro</th>
            <th >nombre</th>
            <th >presentacion</th>
            <th >unidades</th>
            <th >precio</th>
            
          </tr>
            </thead>
            
            
            
    </DataTable>
-->
        
  <v-dialog
    v-model="dialog"
    persistent
    fullscreen
  >
  <v-card>
  
<!--Empieza Buscador-->
 
     
<div class="content">  
       <div class="row shadow p-3" >
              <div class="col-9 text-center ">
                <!--<input type="text" v-model="buscar" class="form-control" placeholder="Busqueda por nombre de medicamento"/>  --> 
                <v-text-field  v-model="buscar" label="Busqueda por nombre de medicamento" variant="underlined" block></v-text-field>
              </div>
              <div class="col-3 text-center "> 
                <v-btn @click="BuscarMedicamento()" color="primary" prepend-icon="mdi-magnify" block>Buscar</v-btn>  
              </div>
              
            </div>
</div>             
                <!--FIN-->                  


                <div class="containerScroll">
    <div class="content" ref="scrollContainer">
<div class="row mt-5">

  <div class="col-md-4" v-for="item in ListaFormularios" v-bind:key="item.nroRegistro"> 

    <div class="card mb-4 ">
      
      <div class="card-body"><v-icon start icon="mdi-arrow-right" ></v-icon>
     {{ item.nombre }} -  {{ item.presentacion }}   
      
        
          <div class="row" >
              <div class="col-6 text-left "><strong>$</strong> {{ item.precio }} </div>
              <div class="col-6 text-center ">
                <v-btn fab  @click="Mostrar(  item.nombre, item.presentacion, item.precio)" color="primary" prepend-icon="mdi-open-in-new">Seleccionar</v-btn>
              </div>
          </div>
          
 

        
      </div>
     
    </div>

  </div>

</div>
</div>

</div>
Medicamento Seleccionado
<div class="row" >
              <div class="col-3 text-center ">
                
                <v-text-field  v-model="MedCodigo"  variant="underlined" block></v-text-field>
              </div>
              <div class="col-5 text-center ">
                
                <v-text-field  v-model="MedPresentacion"  variant="underlined" block></v-text-field>
              </div>
              <div class="col-2 text-center "> 
                <v-text-field  v-model="MedPrecio"  variant="underlined" block></v-text-field>
              </div>
              <div class="col-2 text-center "> 
                <v-text-field  v-model="MedCantidad" label="Ingresar cantidad" variant="underlined" block></v-text-field>
              </div>
              
            </div>
<!--Termina Buscador-->
  <v-card-actions>
            <v-spacer></v-spacer>
            
            <v-btn
              color="blue-darken-1"
              variant="text"
              @click="cerrarventana()"
              
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
<!-- Empieza tabla con paginador -->
<input type="text" v-model="searchQuery" placeholder="Buscar..." />

<table class="table  " id="m25"  >
                <thead>
                    <tr>
                        <th>Identificador</th>
                        <th scope="col" v-for="Encabezados of dataHeaders">{{ Encabezados }}</th>
                        <th scope="col"> Acciones </th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="Datos in dataValues">
                        <td> {{ Datos[0] }}</td>
                        <td scope="col" v-for="valor in Datos.slice(1)">{{ valor.value }}</td>
                        <td class="nowrap">
                            <div class="row">
                                <div class="col-auto"> 
                                    <v-btn class="btn btn-primary mx-1 btn-sm" title="Editar" @click="mostrardialogEdicion(Datos)" v-if="$store.state.permisos.includes(10)">
                                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                            class="bi bi-pencil-fill" viewBox="0 0 16 16">
                                            <path
                                                d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z" />
                                        </svg>
                                    </v-btn>
                                </div>
                                <div class="col-auto">
                                    <v-btn class="btn btn-danger mx-1 btn-sm" title="Eliminar"
                                        @click="mostrarConfirmacionEliminar(Datos[0])" v-if="$store.state.permisos.includes(12)">
                                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                            class="bi bi-trash-fill" viewBox="0 0 16 16">
                                            <path
                                                d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z" />
                                        </svg>
                                    </v-btn>
                                </div>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>

    <div class="pagination">
      <button @click="prevPage" :disabled="currentPage === 1">Anterior</button>
      <span>Página {{ currentPage }} de {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Siguiente</button>
    </div>

   
</template>
<script>

//import datos from "../assets/json/pokemones.json";
import ejemplo from '../components/ejemplo.vue';
import BarraNavegacion from '@/components/BarraNavegacion.vue';
import Spinner from '@/components/Spinner.vue';
import AlertaSuceso from '@/components/AlertaSuceso.vue';
import EditarFilaModal from '../components/EditarFilaModalN.vue';
import DataTable from 'datatables.net-vue3'
import Select from 'datatables.net-select';
import DataTablesCore from 'datatables.net-bs5';
import Buttons from 'datatables.net-buttons-bs5';
import 'datatables.net-responsive-bs5';



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
    'alerta-suceso': AlertaSuceso,
     DataTable
  },
  name: 'Pokemones',
  props: {
    msg: String
  },
  
  data: function () {
    return {
    //-----------------------------
    //-----------------------------
    searchQuery: '',
      currentPage: 1,
      itemsPerPage: 5,
      items: [
        { dato1: 'Dato 1', dato2: 'Dato 2', dato3: 'Dato 3' },
        { dato1: 'Dato 4', dato2: 'Dato 5', dato3: 'Dato 6' },
        { dato1: 'Dato 7', dato2: 'Dato 8', dato3: 'Dato 9' },
        { dato1: 'Dato 10', dato2: 'Dato 11', dato3: 'Dato 12' },
        { dato1: 'Dato 13', dato2: 'Dato 14', dato3: 'Dato 15' },
        { dato1: 'Dato 16', dato2: 'Dato 17', dato3: 'Dato 18' },
        { dato1: 'Dato 19', dato2: 'Dato 20', dato3: 'Dato 21' },
        { dato1: 'Dato 22', dato2: 'Dato 23', dato3: 'Dato 24' }
        // Más datos según sea necesario
      ],

    //-----------------------------
    //-----------------------------
      selectedItem: '', // Elemento seleccionado inicialmente
      items: ['Elemento1', 'Elemento2', 'Elemento3'], // Lista de elementos
    
      VerDatosText: '',
      //ValorCombo: {},//<-- el seleccionado estará aquí
      ValorCombo: '',
      ValorCombo1: '',
      docentes: [], // <-- La lista de docentes
      ListObraSocial:[],
      codigo:'',
      nombre:'',
      valor:'',
      buscar: '',
      //filter: null,
      //filterOn: [],
      selected: [],
      arreglobuscador: [],
      dialog: false,  
      selectedId: -1,
        selectedRow: '',
       //************ */
       //***Control de texto */
       lengthRules: [
        value => {
          if (  /[0-9-]+/.test(value) && value?.length > 5) return true
            return 'Acepta valores numericos y mas de 5 digitos.'
        },
      ],
       //************ */
        
      columns:[
        {data:'troquel',text: 'troquel', value: 'troquel', sortable: true},
        {data:'codBarras',text: 'codBarras', value: 'codBarras', sortable: true},
        {data:'nroRegistro', text: 'nroRegistro', value: 'nroRegistro', sortable: true },
        {data:'nombre', text: 'nombre', value: 'nombre', sortable: true },
        {data:'presentacion', text: 'presentacion', value: 'presentacion', sortable: true },
        {data:'unidades', text: 'unidades', value: 'unidades', sortable: true },
        {data:'precio', text: 'precio', value: 'precio', sortable: true },
        {data:null,
        render: function (data, type, row, meta) {
          return `-`
        }}
      ], 
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
      mensajeAlertaSuceso:"",
      idConfigFormToDelete: null,
      string_id:"",
      default_value: "",
      value_list: "",
      mask_library: "",
      assumed_value: "",
      length: "",
      VerDatos: "",
      MedCodigo:"",
      MedPresentacion:"",
      MedNombre:"",
      MedPrecio:"",
      Numero:"",
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
    
    
  },
  computed: {
           
 //--------------------------
 //--------------------------
 filteredItems() {
      if (!this.searchQuery) {
        return this.items;
      }
      const query = this.searchQuery.toLowerCase();
      return this.items.filter(item => {
        return (
          item.dato1.toLowerCase().includes(query) ||
          item.dato2.toLowerCase().includes(query) ||
          item.dato3.toLowerCase().includes(query)
        );
      });
    },
    paginatedItems() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.filteredItems.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.filteredItems.length / this.itemsPerPage);
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
        Mostrar(V1, V2, V3){
        
          this.MedCodigo = V1;
          this.MedPresentacion =V2;
          this.MedPrecio = V3;
          
        },
    limpiar(){
      this.string_id = "";
      this.default_value ="";
      this.value_list ="";
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
    AgregarMed(){
        
        this.dialog = true;
        
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
      this.VerDatosText = "Riveros Hugo Adrian - Obra Social: Medife - Plan: Bronce";
      this.ValorCombo = "1130";
      this.ValorComboOrigen = "2258";
      this.selectedItem = "Elemento2";
    } else {
        alert('Por favor ingresa un número antes de presionar "Enter"');
      }
      // Aquí puedes agregar la lógica que deseas ejecutar cuando se presione "Enter"
    },
    verId(){
      alert("Hola")
    },
    async BuscarMedicamento() {
      
      this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
      const respuesta = await this.axios.get(`/api/ConfigForm/BuscaAlfaBetaNombre?pNombre=${this.buscar}`, {
    timeout: 100000 // Tiempo de espera en milisegundos (10 segundos en este caso)

   
    
  })
        .then((respuesta) => {
          this.ListaFormularios = respuesta.data.lista
          //console.log("Importante Lista ListaFormularios");
          //console.table(this.ListaFormularios);
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
        
            
      this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
    },
    async MostrarCombo() {
      
      this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=2&pId=0")
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
      //alert("Agrega Campo");
        //await this.axios.post(`/api/ConfigForm/AgregarCampos/1/0/${this.default_value}/${this.value_list}/${this.mask_library}/${this.assumed_value}/${this.length}`)
        //Funciona Correcto
        await this.axios.post(`/api/ConfigForm/AgregarCampos/1/0/${this.default_value}/${this.value_list}/${this.mask_library}/${this.assumed_value}/${this.length}`)
        .then(datos => {
          this.mostrarAlertaEliminar = false;
          this.mensajeAlertaSuceso = "Grabaron Correctamente los datos";
          this.mostrarAlertaSuceso = true;
         

          setTimeout(() => {
                   this.mostrarAlertaSuceso = false;
                }, 5000);
        });
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