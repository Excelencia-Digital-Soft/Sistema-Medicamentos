<template>

  <barra-navegacion></barra-navegacion>
  <!--
Menu nuevo
<v-app-bar>
  Editor de Vue
</v-app-bar>

   
   <v-layout>
   <v-app-bar>
  Editor de Vue
</v-app-bar>
</v-layout>-->


  <v-img
          :src="require('../assets/LogoExc.png')"
          class="my-3"
          contain
          height="330"
          style="z-index: -1;"
          
        ></v-img>
        <br><br>
        <div class="row" >
            <div class="col  p-3  ">
             <v-card
                href="/Medicamentos" 
                class="mx-auto"
            
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de Articulos
                </template>

                <v-card-text>
                  Carga de Articulos asociados a AlfaBeta
                </v-card-text>
              </v-card>
              
              </div>
              <div class="col  p-3  ">
             <v-card
                href="/Add" 
                class="mx-auto"
            
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de Consumos
                </template>

                <v-card-text>
                  Carga de Consumo de medicamentos
                </v-card-text>
              </v-card>
              
              </div>
         </div>
        
          <div v-show="isVisible">
        <div class="row" >
            <div class="col  p-3  ">
             <v-card
                href="/TipoString" 
                class="mx-auto"
            
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de StringType
                </template>

                <v-card-text>
                  Carga de StringType
                </v-card-text>
              </v-card>
              
              </div>
              <div class="col  p-3  ">
               

              <v-card
                href="/TipoInteger" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de IntegerType
                </template>

                <v-card-text>
                  Carga de IntegerType
                </v-card-text>
              </v-card>
                
              </div>
              <div class="col  p-3  ">
                <v-card
                href="/TipoDouble" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de DoubleType
                </template>

                <v-card-text>
                  Carga de IntegerType
                </v-card-text>
              </v-card>
             
                
              </div>
        </div>
      
        <div class="row" >
            <div class="col  p-3  ">
              <v-card
                href="/TipoBoolean" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de BooleanType
                </template>

                <v-card-text>
                  Carga de BooleanType
                </v-card-text>
              </v-card>
              </div>
              <div class="col  p-3  ">
                <v-card
                href="/TipoLabel" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de LabelType
                </template>

                <v-card-text>
                  Carga de LabelType
                </v-card-text>
              </v-card>
              </div>
              <div class="col  p-3  ">
                <v-card
                href="/TipoText" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de TextType
                </template>

                <v-card-text>
                  Carga de TextType
                </v-card-text>
              </v-card>
              </div>
        </div> 
        <div class="row" >
          <div class="col  p-3  ">
                <v-card
                href="/TipoDate" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de DateType
                </template>

                <v-card-text>
                  Carga de DateType
                </v-card-text>
              </v-card>
              </div>
              <div class="col  p-3  ">
                <v-card
                href="/TipoTime" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de TimeType
                </template>

                <v-card-text>
                  Carga de TimeType
                </v-card-text>
              </v-card>
              </div>
              <div class="col  p-3  ">
                <v-card
                href="/TipoDateTime" 
                class="mx-auto"
                
                prepend-icon="mdi-play"
                color ="#003366"
              >
                <template v-slot:title>
                  Carga de DateTimeType
                </template>

                <v-card-text>
                  Carga de DateTimeType
                </v-card-text>
              </v-card>
              </div>

        </div>    
      </div> 
        

      
   
</template>
<script>
import BarraNavegacion from '@/components/BarraNavegacion.vue';
export default{
  components:{
        'barra-navegacion': BarraNavegacion,
    },
    data() {
    return {
      isVisible: false,
      items: [
        { dato1: 'Dato 1', dato2: 'Dato 2', dato3: 'Dato 3' },
        { dato1: 'Dato 4', dato2: 'Dato 5', dato3: 'Dato 6' }
        // Más datos según sea necesario
      ]
    };
  },
  mounted() {
    this.setRoleAttribute();
  },
  methods: {
    setRoleAttribute() {
      if (this.$refs.table) {
        this.$refs.table.setAttribute('role', 'grid');
      }
    },
    async fetch() {
            
            
            
            
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
                
        },
        mostrarConfirmacionEliminar(id_fila) {
            this.idFilaAEliminar = id_fila;
            this.mostrarAlertaEliminar = true;
        },
  }
}

</script>
<!-- Inicializaci�n de DataTables -->

<style>
.background-container {
  /* Establece la imagen de fondo */
  background-image: url('../assets/FondoEditor.jpg'); 
  
  /* Ajusta el tamaño de la imagen de fondo según tus necesidades */
  background-size: 1024px 1024px;
  
  /* Centra la imagen de fondo */
  background-position: center;
  background-repeat: no-repeat;
  /* Establece una altura y anchura mínimas para el contenedor */
  min-height: 100vh; /* Ajusta la altura mínima según tus necesidades */
  min-width: 100%; /* Ajusta la anchura mínima según tus necesidades */
  
  /* Otros estilos de diseño si es necesario */
  color: white; /* Color del texto */
  font-size: 12px; /* Tamaño de fuente del texto */
}

/* Otros estilos de CSS para tu contenido, si es necesario */
</style>
