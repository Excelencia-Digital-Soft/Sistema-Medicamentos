<template>
     <div class="container-sm" style="max-width: 1300px; ">
    <v-chip class="d-flex  darken-1 sm"   elevation="1"   >   
            
           <div v-for="formulario of daform" :key="formulario.idConfigForm">
            <b>   {{ formulario.titulo }} </b>   {{ formulario.descripcion }}
       </div>
     </v-chip>
          
     
      <div id="ContenedorDeCampos" > 
            <div class="form-group bg-white "  >
              
            <div  class="shadow p-3 mb-5  rounded table-container text-sm" style="color:#000000; max-width: 1400px;" >
            <!-- Empieza listado de compos de cada formulario -->
            <div class="row">
              <div v-for="campos of dafield" :key="campos.id_Field" :class="campos.posi">
                 <label class="badge bg-secondary left-aligned-text" :for="campos.nombre">{{ campos.etiqueta }}</label>
                <!--Si el tipo es "select", renderiza un select -->
                
                <select :v-model="campos.nombre" v-if="campos.tipo === 'select'"   :class="campos.clase"
            :required="campos.requerido" :identificador="campos.id_Field">
            <option value="">Seleccione {{campos.nombre}} </option>
            <option v-for="Combo in this[campos.opciones.trim()]" :value="Combo.codigo">{{Combo.nombre}}</option>
          </select> 
               
                <!-- Si el tipo es text renderiz aun area de texto -->
                <textarea v-else-if="campos.tipo === 'textarea'"
                :name="campos.nombre"
                :class="campos.clase"
                :required="campos.requerido"
                :identificador="campos.id_Field">
                </textarea>
                <!-- Si el tipo es checkbox, renderiza una casilla de verificación -->
                <input type="checkbox" v-else-if="campos.tipo === 'checkbox'" 
                :name="campos.nombre"
                :class="form-check"
                :required="campos.requerido"
                :identificador="campos.id_Field">
                <!-- Si no, renderiza los demas tipos de input
              -->
                <v-text-field 
                v-else :type="campos.tipo" 
                :placeholder="campos.marcador" 
                :v-model="campos.nombre" 
                :name="campos.nombre"
                @keydown.enter="this[campos.opciones] && this[campos.opciones]($event)"   
                :required="campos.requerido" 
                :identificador="campos.id_Field"
                variant="underlined" block clearable autocomplete="off"
                >
            </v-text-field>
            
              </div>
            </div>
            <!-- FIN Listado de campos -->
            
            </div>
            </div>
      </div>
       <!--Listado de Botones-->
 <v-row>

 <div v-for="formulariobot of dabotones" :key="formulariobot.idConfigForm">
    
  <v-col cols="auto" class="col-3">
 
  <v-btn 
  :prepend-icon="formulariobot.icono"  
   block title="Grabar Datos" 
  :color="formulariobot.color"
  @click="handleClick(formulariobot.metodo)"
   v-if="$store.state.permisos.includes(10)">
    {{ formulariobot.texto }} 
   </v-btn>
   </v-col>
</div>
</v-row>
    </div>
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
                <v-btn @click="Grabar()" prepend-icon="mdi-cloud-upload" color="#FFFFFF"  >Confirma Grabar</v-btn>
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
     <!-- Componente Alerta de suceso -->
     <AlertaSuceso  :visible = "mostrarAlertaSuceso" :mensaje = "mensajeAlertaSuceso"/>
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
            dabotones: null,
          daform: [],
          ListaFormularios: null,
          datos: null, //Datos del Buscador
          ListaCombos: [],
          ListaCombosSector:'',
          ComboListaTipoMedicamento:'',
          ListaCombosI:'',
          ListaCombosII:'',
          filaEditadaPorNombre: {}, // Objeto para mostrar en el formulario HTML
          filaEditadaPorIdAnswer: {}, // Objeto para enviar a la API
          dafield: [],
          id_DelFormulario: null,
          id_DeFila: null,
          loading: false, // Agregamos la variable de loading para controlar el spinner
          datosDeLaFila: null, // Agregar esta línea
          mostrarAlertaSuceso: false, // visibilidad alerta de suceso
          VentanaGrabar: false,
          mensajeAlertaSuceso: ""  //mensaje de alerta de suceso vacio
        };
      },
      created() {
        this.MOstrarDatosForm();
        this.ComboSector();
        this.MostrarCombo();
        this.MostrarComboI();
        this.MostrarComboII();
        this.MostrarComboIII();
        this.ComboTipoMedicamento();
        this.fetch_valores();
        this.fetch_botones();
        
      },
    
      methods: {
        cerrarGrabar() {
            this.VentanaGrabar = false;
        },
        handleClick(functionName) {
      if (typeof this[functionName] === 'function') {
        this[functionName]();
      } else {
        console.error(`Function ${functionName} does not exist`);
      }
    },
        async Grabar() {
        
     
        // Obtén una referencia al contenedor de campos dinámicos
        var contenedor = document.getElementById("ContenedorDeCampos");
        // Encuentra todos los elementos de formulario dentro del contenedor
        var campos = contenedor.querySelectorAll("input[type='text'], textarea, input[type='number'], select, input[type='password'], input[type='date'], input[type='time'], input[type='email'], input[type='checkbox']");
        // Crea un objeto para almacenar los valores
        var valores = [];
        //recuperar valor del idConfigForm
        var idConfigForm = this.$route.params.idConfigForm;
        // Recorre los campos y obtén sus valores
        campos.forEach(function (campo) {
        valores.push({
        id_ConfigForm: idConfigForm,  // Puedes ajustar este valor según tus necesidades
        Campo: campo.getAttribute("v-model"),  // Utiliza getAttribute para obtener el valor de key
        valor: campo.value,
        tipo: campo.getAttribute("type"),
        });    
        
        });
      
        var variable = "";
        var variable_valor = "";
        var valor_sql = "";
        var v = "";
        for (var i = 0; i < valores.length; i++) {
          variable = variable +","+ valores[i].Campo;
          if(valores[i].tipo == "text")
            v = "'"+ valores[i].valor+"'";
        else
        v = valores[i].valor;
  
          variable_valor = variable_valor+","+v;
          
        }
        console.log(idConfigForm);
        //console.log(variable.slice(1));
        //console.log(variable_valor.slice(1));
        var pvariable = variable + ", usuario";
        var pvariable_valor = variable_valor + ","+this.idUsuario;
        console.log(pvariable.slice(1));
        console.log(pvariable_valor.slice(1));  
            await this.axios.post(`api/ConfigForm/AgregarTablas/${idConfigForm}/${pvariable.slice(1)}/${pvariable_valor.slice(1)}`)
            
            .then(datos => {
              this.mostrarAlertaEliminar = false;
              this.mensajeAlertaSuceso = "Grabaron Correctamente los datos";
              this.mostrarAlertaSuceso = true;
              this.VentanaGrabar = false;
             setTimeout(() => {
                     this.mostrarAlertaSuceso = false;
                  }, 5000);
            });
        },
        VerGrabar() {
            
            this.VentanaGrabar = true;
            this.mostrarAlertaGrabar = true;
        },
        async fetch_valores() {
          const idConfigForm = this.$route.params.idConfigForm;
          await this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/${idConfigForm}`)
            .then((respuesta) => {
              this.daform = respuesta.data;
              this.dafield = respuesta.data.datosField;
              })
            .catch(err => {
              console.log(err);
            }).finally(() => {
             });
        },
        async MostrarCombo() {
          const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2129")
            .then((respuesta) => {
              this.ListaCombos = respuesta.data.lista;
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
           })
            .catch(err => {
              console.log(err);
            });
       },
       async fetch_botones() {
       
       const idConfigForm = this.$route.params.idConfigForm;
       
       await this.axios.get(`/api/ConfigForm/ListaBotones?pTipo=${idConfigForm}`)
         .then((respuesta) => {
           this.dabotones = respuesta.data.lista;
           })
         .catch(err => {
           console.log(err);
         }).finally(() => {
          });
     },
       async MostrarComboI() {
            const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2131")
            .then((respuesta) => {
              this.ListaCombosI = respuesta.data.lista;
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
        }, 
       
        async ComboTipoMedicamento() {
         const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2130")
            .then((respuesta) => {
              this.ComboListaTipoMedicamento = respuesta.data.lista;
              //si no hay formularios en la respuesta de la api mostrar mensaje
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
        }, 
        obtenerValores() {
    
    // Obtén una referencia al contenedor de campos dinámicos
    var contenedor = document.getElementById("ContenedorDeCampos");
    
    // Encuentra todos los elementos de formulario dentro del contenedor
    var campos = contenedor.querySelectorAll("input[type='text'], textarea, input[type='number'], select, input[type='password'], input[type='date'], input[type='time'], input[type='email'], input[type='checkbox']");
    
    // Crea un objeto para almacenar los valores
    var valores = [];
    
    //recuperar valor del idConfigForm
    var idConfigForm = this.$route.params.idConfigForm;
    
    // Recorre los campos y obtén sus valores
    campos.forEach(function (campo) {
      valores.push({
        id_ConfigForm: idConfigForm,  // Puedes ajustar este valor según tus necesidades
        id_Field: campo.getAttribute("identificador"),  // Utiliza getAttribute para obtener el valor de key
        valor: campo.value,
      });
    console.log("Muestro identificador");
    console.log(campo.getAttribute("identificador"));
    console.log("Muestro arreglos");
    console.log(campo.value);
    });
    //enviar valores a la api
    // Realiza una solicitud POST a la API para guardar los registros
    this.axios.post('/api/ConfigForm/Respuestas/Guardar', valores)
      .then((respuesta) => {
    
        //redirigir a la grilla dinamica
        //this.$router.push(`/grilla/${idConfigForm}`);
       
       //-----------
        this.mostrarAlertaGrabar = false;
        this.mostrarAlertaEliminar = false;
        this.mensajeAlertaSuceso = "Se Grabaron Correctamente los datos";
        this.mostrarAlertaSuceso = true;
        setTimeout(() => {
                       this.mostrarAlertaSuceso = false;
                    }, 5000);
        //this.fetch();
         //-----------
    
      })
      .catch(err => {
        console.log('Error al guardar los registros:', err);
      });
    
    
    },
        async MostrarCombo() {
          
          //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
          const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2129")
            .then((respuesta) => {
              this.ListaCombos = respuesta.data.lista;
              
              //console.log("Lista Combos ListaCombos");
              //console.log(this.ListaCombos);
             
              //si no hay formularios en la respuesta de la api mostrar mensaje
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
            
                
          //this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
        },   
        
        async MostrarComboII() {
          
          //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
          const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2130")
            .then((respuesta) => {
              this.ListaCombosII = respuesta.data.lista;
              
              //console.log("Lista Combos ListaCombosI");
              //console.log(this.ListaCombosII);
             
              //si no hay formularios en la respuesta de la api mostrar mensaje
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
            
                
          //this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
        }, 
        async MostrarComboIII() {
          
          //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
          const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2130")
            .then((respuesta) => {
              this.ListaCombosII = respuesta.data.lista;
              
              //console.log("Lista Combos ListaCombosI");
              //console.log(this.ListaCombosII);
             
              //si no hay formularios en la respuesta de la api mostrar mensaje
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
            
                
          //this.MostrarSpinner = false;//cerrar spinner cuando termine de realizar la solicitud
        }, 
        async ComboSector() {
          const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2135")
            .then((respuesta) => {
              this.ListaCombosSector = respuesta.data.lista;  
              if (this.ListaFormularios.length == 0) {
                this.NoHayRegistros = true
              }
            })
            .catch(err => {
              console.log(err);
            });
        }, 
        async MOstrarDatosForm() {
          this.id_DelFormulario = this.$route.params.idConfigForm;;
          //this.id_DeFila = this.fila[0];
    
          // Solicitud que trae los datos para construir el formulario
          await this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/${this.id_DelFormulario}`)
            .then((estructuraDelFormulario) => {
              //console.log("Muestra los datos EDITAR");
              this.dafield = estructuraDelFormulario.data.datosField;
              //console.log(this.dafield);
            })
            .catch(err => {
              console.log(err);
            })
            .finally(() => {
              // Finaliza el spinner
              this.loading = false;
            });
        },
        async fetch() {
          // Inicializa el spinner
    
          this.loading = true;
    
          this.id_DelFormulario = this.fila[1].id_ConfigForm;
          this.id_DeFila = this.fila[0];
    
          // Solicitud que trae los datos para construir el formulario
          await this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/${this.id_DelFormulario}`)
            .then((estructuraDelFormulario) => {
              //console.log("Muestra los datos EDITAR");
              this.dafield = estructuraDelFormulario.data.datosField;
              //console.log(this.dafield);
            })
            .catch(err => {
              console.log(err);
            })
            .finally(() => {
              // Finaliza el spinner
              this.loading = false;
            });
    
          // Solicitud que trae los datos de la fila seleccionada
          await this.axios.get(`/api/ConfigForm/ListaRespuestasIdentificadorFila/${this.id_DelFormulario}/${this.id_DeFila}`)
            .then((DatosFila) => {
              this.datosDeLaFila = DatosFila.data.lista; // Asignar a datosDeLaFila
              console.log("Muestra los datos EDITAR");
              console.log(this.datosDeLaFila);
              this.filaEditadaPorNombre = {};
              this.filaEditadaPorIdAnswer = {};
    
              this.datosDeLaFila.forEach((campo) => {
               
              this.filaEditadaPorNombre[campo.nombre] = campo.valor;
              this.filaEditadaPorIdAnswer[campo.id_Answer] = campo.valor;
              //alert(this.filaEditadaPorIdAnswer[campo.id_Answer], this.filaEditadaPorNombre[campo.nombre] );
              });
    
            })
            .catch(err => {
              console.log(err);
            });
        },
        BuscadorEnter(event) {
        // Acceder al contenido del input "NInternado"
        //alert("metodo enter");
        const contenidoNInternado = event.target.value;
        //alert(contenidoNInternado);
        // Asignar el contenido del input "NInternado" al input "DetalleInternado"
        const inputDetalleInternado = document.getElementsByName("detalleInternado")[0];
        if (contenidoNInternado) {
          inputDetalleInternado.value = "Riveros Hugo Adrian - Obra Social: Medife - Plan: Bronce";
        }
        else {
            //alert('Por favor ingresa un número antes de presionar "Enter"');
            inputDetalleInternado.value = "";
            this.mostrarModal = false;
               this.mensajeAlertaSuceso = "Por favor ingresa un número antes de presionar Enter";
               this.mostrarAlertaSuceso = true;
              //sacar alerta de suceso despues de los 1000 milisegundos
              setTimeout(() => {
              this.mostrarAlertaSuceso = false;
              }, 3000);
          }
        },
        
        cerrarModal() {
          this.$emit('cerrar-modal');
        },
        async guardarEdicion() {
          if (this.datosDeLaFila) {
            const ediciones = [];
            for (const campoNombre in this.filaEditadaPorNombre) {
              const campo = this.datosDeLaFila.find(item => item.nombre === campoNombre);
              
              if (campo) {
                const id_Answer = campo.id_Answer;
                ediciones.push({
                id_Answer: id_Answer,
                valor: this.filaEditadaPorNombre[campoNombre].toString()
                }
              );
              }
            }
            //console.log("Muestra los datos a modificar");
            //console.log(ediciones);
            await this.axios
              .post("/api/ConfigForm/Respuestas/Editar", ediciones)
              .then((response) => {
                // Procesar la respuesta del servidor si es necesario
                this.$emit('edicion-guardada');
              })
              .catch((err) => {
                console.error("Error al guardar las ediciones:", err);
                // Manejar el error apropiadamente
              });
          }
    
    
        }
    
      }
    }
    </script>
    
    <style scoped>
    /* Estilos específicos para el componente EditarFilaModal */
    .modal {
      
      
    
      display: flex;
      
      
    }
    .modal-body
    {
      background: #eeecec;
      width: 1200px;
    }
    .modal-dialog {
      
     
      width: 1200px;
    }
    .modal-content{
      
      background: hsl(180, 20%, 99%);
      width: 1200px;
    }
    /* Estilos para el formulario y botones dentro del modal */
    .form-group {
      margin-bottom: 1px;
    }
    
    /* Estilos para el pie del formulario (botones) */
    .modalFooter{
      margin-top: 1px;
    }
    
    /* ...otros estilos... */</style>