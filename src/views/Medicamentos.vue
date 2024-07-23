<template class=" text-center">
  <barra-navegacion></barra-navegacion>

  <v-card  class="px-4 py-2  text-center w-100 bg-light" elevation="3"  style="max-width: 1350px; ">
    
<div  class="shadow p-3  bg-light text-sm text-left" align-center style="max-width: 1350px; " >
  <v-alert
          shaped
        color="#F5F5F5"
        theme="dark"
        icon="mdi-domain"
        density="compact"
        elevation="4"
        border="top"
      >
       <b> Articulos:  </b> 
  
       Carga de articulos asociados a AlfaBeta
      </v-alert>
      <br>
      <!-- ingreso de datos -->
<div class="row bg-white" >
  <div class="col-1" >
  <v-text-field v-model="nroarticulo" label="Identificador"  variant="underlined" size="small" ></v-text-field>
</div>
  <div class="col-1" >
  <v-text-field v-model="codigo" label="codigo" variant="underlined" size="small" ></v-text-field>
</div>

<div class="col-5" >
  <v-text-field  name="Nombre" v-model="Nombre" label="Nombre" variant="underlined" size="small" ></v-text-field>
</div>

<div class="col-1" >
  <v-text-field v-model="NroRegistro" label="NroRegistro" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-1" >
  <v-text-field v-model="troquel" label="troquel" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-2" >
  <v-text-field v-model="barra" label="barra" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-1" >
  <v-text-field v-model="Precio" label="Precio" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-3 text-left" >
      Selecciona un sector
      <select v-model="ValorCombo" class="form-select" id="Combo" >
        <option value="0">Seleccionar un sector...</option> 
        <option v-for="Combo in ListaCombos" :key="Combo.codigo"  :value="Combo.codigo">{{Combo.codigo}} -- {{Combo.nombre}}</option>
      </select>  
       
</div>
<div class="col-3 text-left" >
      Selecciona un Tipo de Medicamento
      <select v-model="ValorComboTipo" class="form-select" id="Combo" >
        <option value="0">Seleccionar un Tipo de Medicamento...</option> 
        <option v-for="Combo in ComboListaTipoMedicamento" :key="Combo.codigo"  :value="Combo.codigo">{{Combo.codigo}} -- {{Combo.nombre}}</option>
      </select>  
       
</div>
<div class="col-2" >
  <v-text-field v-model="stockminimo" label="stockminimo" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-2" >
  <v-text-field v-model="stockmedio" label="stockmedio" variant="underlined" size="small" ></v-text-field>
</div>
<div class="col-2" >
  <v-text-field v-model="stockmaximo" label="stockmaximo" variant="underlined" size="small" ></v-text-field>
</div>

</div>
<!-- COMPONENTE Busca en AlfaBeta --> 




 <v-chip class="d-flex  darken-1 sm"  color="#000000" elevation="1"   >
 <b> Buscador de Medicamentos en AlfaBeta</b>
</v-chip>

<div class="content" >  
       <div class="row shadow p-3 bg-white" >
              <div class="col-9 text-center " >
                
                <v-text-field  v-model="buscar" label="Busqueda por nombre de medicamento de AlfaBeta" variant="underlined" block></v-text-field>
              </div>
              <div class="col-3 text-left "> 
               <!--
                <v-btn @click="BuscarMedicamento()" class="bg-primary" p prepend-icon="mdi-cloud-upload" block>Buscar en AlfaBeta</v-btn> 
             -->
             
                <v-card
                @click="BuscarMedicamento()" 
                class="mx-auto"
                elevation="10"
                prepend-icon="mdi-magnify" 
                color ="primary"
              >
                <template v-slot:title>
                 Buscar
                </template>

                <v-card-text>
                  Buscar medicamento en AlfaBeta
                </v-card-text>
              </v-card>
             
              </div>
              
            </div>
</div>
<div >
    <div class="content" ref="scrollContainer">
      <div class="row mt-5  shadow p-3" >
        <div class="col-md-4 shadow p-3" v-for="item in ListaFormulariosMed" v-bind:key="item.nroRegistro" @click="Mostrar(  item.nombre, item.precio, item.nroRegistro, item.presentacion,item.codBarras,item.troquel)"> 
          <div class="card mb-4 bg-primary shadow p-3">
            <div class="card-body"><v-icon start icon="mdi-arrow-right" ></v-icon>
              {{ item.nombre }} -  {{ item.presentacion }}   <br>
              Cdo. Barra: {{ item.codBarras }}   - Troquel:  {{ item.troquel }}  
                <div class="row" >
                  <div class="col-6 text-left "><strong>$</strong> {{ item.precio }} </div>
                  <div class="col-6 text-center ">
                  
                  </div>
            </div>        
         </div>
         </div>
       </div>

</div>
</div>

</div>

<div class="row shadow p-3 bg-white" >
<div class="row bg-white" >
<div class="col-2" ></diV>
  <div class="col-3" >
 <v-btn @click="VerGrabar()" color="primary" p prepend-icon="mdi-checkbox-marked-circle" block>Grabar</v-btn> 
 </div>
 <div class="col-3" >
 <v-btn @click="Limpiar()" color="primary" p prepend-icon="mdi-minus-circle" block>Limpiar</v-btn> 
 </div>
 <div class="col-3">
  <v-btn @click="mostrarConfirmacionEliminar()" color="#FF0000" p prepend-icon="mdi-cancel" block>Eliminar</v-btn> 
</div>
</div>
</div>
<br>
<!-- COMPONENTE Listado de Medicamentos 
<ListarMed />
--> 
<v-chip class="d-flex  darken-1 sm"   elevation="1"   > 
   <b>Listado de Articulos  </b> 

</v-chip>
<div class="row bg-white" >
              <div class="col  p-3 text-center ">
               
                </div>
                <div class="col  p-3 text-center ">
                 
                </div>
                <div class="col  p-3 text-center ">
                    <v-text-field v-model="searchQuery" label="Buscador" append-inner-icon="mdi-magnify" variant="underlined" size="small" ></v-text-field>
                </div>
          </div>
      
      <table class="table table-bordered table-hover bg-white text-left">
        <thead>
          <tr>
            <th v-for="(header, index) in headers" :key="index">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in paginatedRows" :key="rowIndex">
            <td v-for="(header, colIndex) in headers" :key="colIndex">{{ row[header] }}</td>
            <td>
            <v-btn @click="sendRowData(row)" prepend-icon="mdi-pencil" class="bg-primary" >Ver</v-btn>
          </td>
          </tr>
          
        </tbody>
      </table>
      
      <div class="pagination">
        <v-btn @click="prevPage" :disabled="currentPage === 1" class="bg-primary">Anterior</v-btn>
        <span>Página {{ currentPage }} de {{ totalPages }}</span>
        <v-btn @click="nextPage" :disabled="currentPage === totalPages" class="bg-primary">Siguiente</v-btn>
      </div>
      
    </div>
 




 

    <!-- codigo anterios -->



      <spinner :visible="MostrarSpinner"></spinner>
      <div v-if="!MostrarSpinner">
          
          
          <div >
          
          <!--Titulo del Formulario-->
         
          
   
      </div>    
          
      
          
  
             
           <v-dialog
            v-model="dialog"
            persistent
            
             fullscreen
             
            >   
          </v-dialog> 
            <v-card>
             
    aca cartel eliminar
 <div class="col  p-3 text-center">
            
       
             <alerta-suceso  :visible = "mostrarAlertaSuceso" :mensaje = "mensajeAlertaSuceso"/>
      <!--fin alerta suceso-->
           <!-- Alerta de confirmación personalizada -->
        
      <div v-if="mostrarAlertaEliminar"  class="alert alert-primary d-flex align-items-center" role="alert">
        <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Info:">
          <use xlink:href="#info-fill" />
        </svg>
        <div>
          ¿Estás seguro de que deseas eliminar este registro?
          <button class="btn btn-outline-danger btn-sm ms-3" @click="eliminarform(idConfigFormToDelete)">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
              class="bi bi-exclamation-triangle-fill" viewBox="0 0 16 16">
              <path
                d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z" />
            </svg>
            Confirmar</button>
          <button class="btn btn-outline-secondary btn-sm ms-2" @click="cancelarEliminacion">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-square-fill"
              viewBox="0 0 16 16">
              <path
                d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm3.354 4.646L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 1 1 .708-.708z" />
            </svg>
            Cancelar</button>
        </div>
      </div> <!--fin alerta confirmacion-->
   </div>
          
            </v-card>
       
        
  </div>

  <!-- Ventana GRABER -->
 
<v-dialog
            v-model="VentanaGrabar"
            persistent
            width="500"
  > 
  <v-alert
          shaped
        color="#CCCCCC"
        theme="dark"
        icon="mdi-alert"
        density="compact"
        elevation="4"
        border="top"
      >
  <!-- Alerta de confirmación personalizada -->
      <div v-if="mostrarAlertaGrabar"  role="alert">
            <svg class="bi flex-shrink-0 me-2" width="24" height="24" role="img" aria-label="Info:">
                <use xlink:href="#info-fill" />
            </svg>
            <div>
                <div class="row">
                    <div class="col  p-3 text-center ">    
                <v-btn @click="VerGrabar()" prepend-icon="mdi-cloud-upload" color="#FFFFFF"  >Confirma Grabar</v-btn>
          </div>
          <div class="col  p-3 text-center ">
          <v-btn  prepend-icon="mdi-cancel" color="#FF0000" @click="cerrarGrabar">   <v-spacer></v-spacer> Cancelar</v-btn>
        </div>
        </div>
            </div>
        </div>
        
        <!--fin alerta confirmacion obtenerValores-->
    </v-alert>
    </v-dialog>

</v-card>

<v-layout style=" max-width: 100%;">
          <v-footer class="d-flex flex-column w-100" style=" bottom:0px;max-width: 100%;">
    <v-card  class="px-4 py-2 bg-light text-center w-100" elevation="16">
      <strong>© 2024 | Excelencia Digital Sotfware</strong>

      <v-spacer></v-spacer>

    
    </v-card>

 
  </v-footer>  
</v-layout> 
  </template>
  <script>
  
  //import combobox from '../components/combobox.vue';
  import ListarMed from '../components/ListarMed.vue';
  import BuscarMed from '../components/BuscarMed.vue';
  import BarraNavegacion from '@/components/BarraNavegacion.vue';
  import Spinner from '@/components/Spinner.vue';
  import AlertaSuceso from '@/components/AlertaSuceso.vue';
  import DataTable from 'datatables.net-vue3'
  import Select from 'datatables.net-select';
  import DataTablesCore from 'datatables.net-bs5';
  import Buttons from 'datatables.net-buttons-bs5';
  import 'datatables.net-responsive-bs5';

 
  
  import { ref } from 'vue';

  
 
  const table = ref();
  export default {
    ListaFormulariosArticulos:'',
        rows: [],
        searchQuery: '',
        currentPage: 1,
        itemsPerPage: 3,
    arreglobuscador: [],
    name: 'TableCom',
    name: "Formularios",
    components: {
      'spinner': Spinner,
      'barra-navegacion': BarraNavegacion,
      ListarMed,
      BuscarMed,
      //combobox,
      'alerta-suceso': AlertaSuceso,
       DataTable
    },
    name: 'Pokemones',
    props: {
      msg: String
    },
    
    data: function () {
      return {
        nroarticulo:'',
        Codigo: '',
        Nombre: '',
        NroRegistro: '',
        Precio: '',
        ValorCombo: '',
        ValorComboTipo: '',
        ListaCombos: null,
        ListaCombosTipo: null,
        nroRegistro: '',
        buscar: '',
        filter: null,
        filterOn: [],
        selected: [],
        arreglobuscador: [],
        dialog: false,  
        selectedId: -1,
          selectedRow: '',
          //************ */
       //***Control de texto */
       //lengthRules: [
       // value => {
       //   if (  /[0-9-]+/.test(value) && value?.length < 10) return true
        //    return 'Acepta valores numericos y hasta 10 digitos.'
       // },
      //],
       //************ */ 
       ListaFormulariosArticulos:'',
        rows: [],
        searchQuery: '',
        currentPage: 1,
        itemsPerPage: 5,
        titulo_Modal:"",
        Id: null, 
        datos: null,
        ComboListaTipoMedicamento:'',
        ListaFormularios: null,
        MostrarSpinner: false,
        NoHayRegistros: false,
        mostrarAlertaEliminar: false,
        mostrarAlertaSuceso: false,
        VentanaGrabar: false,
        mensajeAlertaSuceso:"",
        idConfigFormToDelete: null,
        idArticulo:"",
        ListaFormulariosMed: null,
        nombre: "",
        codigo: "",
        tipo_Articulo: "",
        precio_Venta: "",
        precio_Costo: "",
        VerDatos: "",
        Entrega:0,
        troquel:"",
        barra: "",
        stockminimo: "",
        stockmedio: "",
        stockmaximo: "",
        
      }
    },
    created() {
      
      this.ValorCombo = "0";
      this.ValorComboTipo = "0";
      this.MostrarCombo();
      //this.MostrarComboTipo();
      this.idUsuario = this.$store.state.id_usuario;
      this.fetchArticulosMed();
      this.ComboTipoMedicamento();
      
      
    },
    computed: {
             
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
      }
              //formTitle () {
            //     return this.Entrega  === 0 ? 'Gargar nuevos datos' : 'Modificar datos'
             // },
          
           //   ListaFormularios1() {
                
             //   return this.datos.filter(item => {
        //  return item.nombre.toLowerCase().includes(this.buscar.toLowerCase());
          
       // });
      //},
           
          },
    methods: {
      ver2024(){
alert("grabar");

    },
      VerGrabar() {
       
            this.VentanaGrabar = true;
            this.mostrarAlertaGrabar = true;
        },
        cerrarGrabar() {
            this.VentanaGrabar = false;
        },
    async sendRowData(row) {
      const keys = Object.keys(row);
      const entries = Object.entries(row);
      const primerpar = entries[0];  // Valor de la columna
      this.nroarticulo = primerpar[1];
      const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulosTodos?pTipo=${this.nroarticulo}`)
          .then((respuesta) => {
            let data = []; //declarar la variable data
            this.ListaFormulariosArticulos = respuesta.data.lista;
            data = respuesta.data.lista;
            data.forEach(item => {
              this.Nombre = item.nombre;
              this.codigo = item.codigo;
              this.NroRegistro = item.nroregistro;
              this.NroRegistro = item.nroregistro;
              this.Precio = item.precio;
              this.ValorCombo = item.sector;
              this.ValorComboTipo = item.tipomedicamentos;
              this.stockminimo = item.stockminimo;
              this.stockmedio = item.stockmedio;
              this.stockmaximo = item.stockmaximo;
              this.troquel = item.troquel;
              this.barra = item.codbarra;
              ;
            });    
          })
          .catch(err => {
            //console.log(err);
          });
     
      
    },
    async ComboTipoMedicamento() {
       const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=3&pId=0")
          .then((respuesta) => {
            this.ComboListaTipoMedicamento = respuesta.data.lista;
            console.log("aca muestra los tipos");
            console.log(this.ComboListaTipoMedicamento);
            //si no hay formularios en la respuesta de la api mostrar mensaje
            if (this.ListaFormularios.length == 0) {
              this.NoHayRegistros = true
            }
          })
          .catch(err => {
            console.log(err);
          });
      },
    async fetchArticulosMed() {
        //alert(this.idUsuario);
        //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud 
        //const respuesta = await this.axios.get("/api/ConfigForm/ListaField?pTipo=2136")
        //const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idConfig}`)
       const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idUsuario}`)
          .then((respuesta) => {
            this.rows = respuesta.data.lista;
            console.log("IMPORTANTE Muestro rows")
            console.table(this.rows);     
          })
          .catch(err => {
            //console.log(err);
          });
      // this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
      },
      prevPage() {
        if (this.currentPage > 1) {
          this.currentPage--;
        }
      },
      nextPage() {
        if (this.currentPage < this.totalPages) {
          this.currentPage++;
        }
      },
      
      onSelect(e, dt, type, indexes ){
       
        this.string_id = indexes;
        this.dialog = true;
        console.log("aca estoy")
            console.log(dt);
          },
          
         Limpiar(){
        this.nroarticulo = "0";
        this.codigo = "";
        this.Nombre = "";
        this.codigo = "";
        this.NroRegistro = "";
        this.NroRegistro = "";
        this.Precio = "";
        this.ValorCombo = "0";
        this.ValorComboTipo = "0";
        this.stockminimo = "";
        this.stockmedio = "";
        this.stockmaximo = "";
        this.troquel = "";
        this.barra = "";
      },
      async MostrarCombo() {
      
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=4&pId=0")
        .then((respuesta) => {
          this.ListaCombos = respuesta.data.lista;
          //si no hay formularios en la respuesta de la api mostrar mensaje
          if (this.ListaFormularios.length == 0) {
            this.NoHayRegistros = true
          }
        })
        .catch(err => {
          console.log(err);
        });
    },
    async MostrarComboTipo() {
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2130")
        .then((respuesta) => {
          this.ListaCombosTipo = respuesta.data.lista;
          //si no hay formularios en la respuesta de la api mostrar mensaje
          if (this.ListaFormularios.length == 0) {
            this.NoHayRegistros = true
          }
        })
        .catch(err => {
          console.log(err);
        });
    },
      nuevo(){
        this.Entrega = 0;
        this.dialog = true;
        this.string_id = "";
        this.default_value ="";
        this.value_list ="";
        this.mask_library = "";
        this.assumed_value = "";
        this.length = "";
      },
      cerrarventana(){
       
        this.dialog = false;
        this.fetch();
      },
      editar(Listaform){
        
        this.Entrega = 1;
        this.dialog = true;
        this.idArticulo = Listaform.idArticulo;
        this.nombre = Listaform.nombre;
        this.codigo = Listaform.codigo;
        this.tipo_Articulo = Listaform.tipo_Articulo;
        this.precio_Venta = Listaform.precio_Venta;
        this.precio_Costo = Listaform.precio_Costo;
        this.stock_Maximo = Listaform.stock_Maximo;
        this.stock_Medio = Listaform.stock_Medio;
        this.stock_Minimo = Listaform.stock_Minimo;
        this.ValorCombo = "San Martin";
        
        this.troquel = Listaform.troquel;
        this.barra = Listaform.barra;
      },
      async fetch() {
        
        this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
        const respuesta = await this.axios.get("/api/ConfigForm/ListarMedicamentosClinicas?pIdClinica=1")
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
      mostrarConfirmacionEliminar(Entrega) {
      
        this.mostrarAlertaEliminar = true;
    this.idConfigFormToDelete = this.string_id; // Guarda el idConfigForm en data
    
      },
      cancelarEliminacion() {
        this.mostrarAlertaEliminar = false;
      },
     
      async Agregar() {
        
        if(this.Entrega == 1)//Modifica
          this.Modificar();//alert("Modiifca Campo");
          else
          this.Grabar();//alert("Agrega Campo");
      },
      async Grabar() {
  
          await this.axios.post(`/api/ConfigForm/AgregarCampos/1/0/${this.default_value}/${this.value_list}/${this.mask_library}/${this.assumed_value}/${this.length}`)
          .then(datos => {
            this.mostrarAlertaEliminar = false;
            this.mensajeAlertaSuceso = "Grabaron Correctamente los datos";
            this.mostrarAlertaSuceso = true;
            //this.fetch();
  
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
            //this.fetch();
  
            setTimeout(() => {
                     this.mostrarAlertaSuceso = false;
                  }, 5000);
          });
      },
       async BuscarMedicamento() {
    const respuesta = await this.axios.get(`/api/ConfigForm/BuscaAlfaBetaNombre?pNombre=${this.buscar}`, {
    
 })
        .then((respuesta) => {
        this.ListaFormulariosMed = respuesta.data.lista
        this.datosMed = this.ListaFormulariosMed;
        console.log("datos de busqueda de alfabeta");
        console.log(this.ListaFormulariosMed);
        console.log("FIN");
        if (this.ListaFormulariosMed.length == 0) {
            alert("No se encontraron datos para la busqueda")
          }
        })
        .catch(err => {
          console.log(err);
        });
    },
      Mostrar(V1, V2, V3, V4, V_barra, V_troquel) {
     this.Nombre = V1 +" -  "+ V4;
     this.NroRegistro = V3;
     this.Precio = V2;
     this.barra = V_barra;
     this.troquel = V_troquel;
     
        const pNombre = document.getElementsByName("Nombre")[0];
        pNombre.value = V1 +" -  "+ V4;
        
        this.ListaFormulariosMed = null;
      
    },
    
      async eliminarform(idConfigFormToDelete) {
        await this.axios.put(`/api/ConfigForm/EliminaCampos/14/${this.nroarticulo}`)
       
          .then(datos => {
            this.mostrarAlertaEliminar = false;
            this.mensajeAlertaSuceso = "Eliminado exitosamente";
            this.mostrarAlertaSuceso = true;
            //this.fetch();
            this.fetchArticulosMed();
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
  </style>