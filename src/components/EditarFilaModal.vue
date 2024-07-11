<template>
 
       
  <div class="modal-header">
    <h5 class="modal-title">Editar Datos</h5>
    
  </div>
  <!--<div class="modal-body">
    <div v-for="campo of dafield" :key="campo.id_Field">
      <label :for="campo.nombre">{{ campo.etiqueta }}</label>
      <input :type="campo.tipo" :placeholder="campo.marcador" :class="campo.clase" :name="campo.nombre"
        :required="campo.requerido" v-model="filaEditadaPorNombre[campo.nombre]">
    </div>
  </div>-->
  <div class="modal-body">
    <!-- Spinner: lo mostramos si loading es true -->
    <div class=" justify-content-center" v-if="loading">
      <div class="spinner-border" role="status">
        <span class="sr-only"></span>
      </div>
    </div>
    <div v-if="!loading">
      <div class="row">
      <div v-for="campo of dafield" :key="campo.id_Field" :class="campo.posi" >
        <label :for="campo.nombre"><b>{{ campo.etiqueta }}</b></label>
       
       
        <select v-model="filaEditadaPorNombre[campo.nombre]" v-if="campo.tipo === 'select'"   :class="campo.clase"
        :required="campo.requerido" :identificador="campo.id_Field">
        <option value="">Seleccione {{campo.nombre}} </option>
        <option v-for="opcion in this[campo.opciones.trim()]" :value="opcion.codigo">{{opcion.nombre}}</option>
        </select>
       <!--
        <select v-if="campo.tipo === 'select'" :name="campo.nombre" :class="campo.clase" :required="campo.requerido"
          v-model="filaEditadaPorNombre[campo.nombre]">
          <option v-for="opcion in campo.opciones ? campo.opciones.split(',') : []" :value="opcion.trim()">{{
            opcion.trim() }}</option>
        </select>
        -->
        <!--
        <v-text-field 
        v-else :type="campo.tipo"
         :placeholder="campo.marcador"
          
           :name="campo.nombre"
           @keydown.enter="this[campo.opciones] && this[campo.opciones]($event)" 
          :required="campo.requerido"
          v-model="filaEditadaPorNombre[campo.nombre]"
          variant="underlined" block
          >
        </v-text-field>
         -->
         <v-text-field 
        v-else :type="campo.tipo"
         :placeholder="campo.marcador"
          
           :name="campo.nombre"
           @keydown.enter="this[campo.opciones] && this[campo.opciones]($event)" 
          :required="campo.requerido"
         v-model="filaEditadaPorNombre[campo.nombre]"
          variant="underlined" block
          >
        </v-text-field>
      </div>
      </div>
      <div class="modalFooter text-center">
        <br>
        <div class="row">
          
<div class="col  p-6 text-center ">
<alerta-suceso  :visible = "mostrarAlertaSuceso" :mensaje = "mensajeAlertaSuceso"/>
</div>
<div class="col  p-6 text-center ">
<v-btn type="button"  class="btn  btn-sm " color="primary" block @click="guardarEdicion"  prepend-icon="mdi-cloud-upload" >Guardar</v-btn>
</div>

</div>


</div> 
      </div>
  </div>

</template>

<script>
import AlertaSuceso from "../components/AlertaSuceso.vue";
export default {
name: 'EditarFilaModal',
components: {
AlertaSuceso,
},
props: {
fila: Object,
campoTexto: String,
},
data() {
return {
ListaCombos: [],
ListaCombosI:'',
ListaCombosII:'',
ComboListaTipoMedicamento:'',
filaEditadaPorNombre: {}, // Objeto para mostrar en el formulario HTML
filaEditadaPorIdAnswer: {}, // Objeto para enviar a la API
dafield: [],
id_DelFormulario: null,
id_DeFila: null,
loading: false, // Agregamos la variable de loading para controlar el spinner
datosDeLaFila: null, // Agregar esta línea
mostrarAlertaSuceso: false, // visibilidad alerta de suceso

mensajeAlertaSuceso: ""  //mensaje de alerta de suceso vacio
};
},
created() {
this.fetch();
this.MostrarCombo();
this.MostrarComboI();
this.MostrarComboII();
this.MostrarComboIII();
this.ComboTipoMedicamento();
},

methods: {
async ComboTipoMedicamento() {
const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=3&pId=0")
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
async MostrarComboI() {

//this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=4&pId=0")
  .then((respuesta) => {
    this.ListaCombosI = respuesta.data.lista;
    
    //console.log("Lista Combos ListaCombosI");
    //console.log(this.ListaCombosI);
   
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
async ComboTipoMedicamento() {
       const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=3&pId=0")
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
async MostrarComboIII() {

//this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2135")
  .then((respuesta) => {
    this.ListaCombosIII = respuesta.data.lista;
    
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
async fetch() {
const entries = Object.entries(this.fila);
const primerpar = entries[0];  // Valor de la columna
this.loading = true;
this.id_DelFormulario = this.$route.params.idConfigForm;
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
const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulosTodos?pTipo=${primerpar[1]}`)
.then((DatosFila) => {
    this.datosDeLaFila = DatosFila.data.lista; // Asignar a datosDeLaFila
    this.filaEditadaPorNombre = {};
    this.filaEditadaPorIdAnswer = {};
    this.datosDeLaFila.forEach(fila => {
      for (let clave in fila) {
          console.log(`Clave: ${clave}, Valor: ${fila[clave]}`);
          this.filaEditadaPorNombre[clave] = fila[clave];
          
          
      }
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
  alert('Por favor ingresa un número antes de presionar "Enter"');
}
},
BuscadorEnter24(event) {
// Acceder al contenido del input "NInternado"
//alert("metodo enter");
const contenidoNInternado = event.target.value;
//alert(contenidoNInternado);
// Asignar el contenido del input "NInternado" al input "DetalleInternado"
const inputDetalleInternado = document.getElementsByName("detalleInternado")[0];
if (contenidoNInternado) {
inputDetalleInternado.value = "Hola Programador";
}
else {
  alert('Por favor ingresa un número antes de presionar "Enter"');
}
},
cerrarModal() {
this.$emit('cerrar-modal');
},


async guardarEdicion() {
  var contenedor = document.getElementById("ContenedorDeCampos");
        // Encuentra todos los elementos de formulario dentro del contenedor
        var campos = contenedor.querySelectorAll("input[type='text'], textarea, input[type='number'], select, input[type='password'], input[type='date'], input[type='time'], input[type='email'], input[type='checkbox']");
        // Crea un objeto para almacenar los valores
        var valores = [];
        //recuperar valor del idConfigForm
        var idConfigForm = this.$route.params.idConfigForm;
        // Recorre los campos y obtén sus valores
        //campos.forEach(function (campo) {
        //valores.push({
        //id_ConfigForm: idConfigForm,  // Puedes ajustar este valor según tus necesidades
       // Campo: campo.getAttribute("v-model"),  // Utiliza getAttribute para obtener el valor de key
       // valor: campo.value,
        //tipo: campo.getAttribute("type"),
        //});    
        
       // });
        //valores[0] = this.filaEditadaPorNombre;
        valores.push(this.filaEditadaPorNombre);
        console.log("ACA los valores valores 123");
       //console.log(valores.length);
        var variable = "";
        var variable_valor = "";
        var valor_sql = "";
        var v = "";
       
        //Object.entries(this.filaEditadaPorNombre).forEach(([clave, valor]) => {
    ///console.log(`Clave: ${clave}, Valor: ${valor}`);
    //variable = variable + {clave};

//});
var primero ="";
for (let clave in this.filaEditadaPorNombre) {
    if (this.filaEditadaPorNombre.hasOwnProperty(clave)) {
        
       primero = primero +  `${clave} = ${this.filaEditadaPorNombre[clave]}`;
       break;
    }

    
}
//console.log(variable);
//console.log(variable_valor);
////////////////////////////
//console.log("aca campos");
//console.log(campos);
const BuscaValor = (abuscar) => {
  let variable = '';
  Object.entries(this.filaEditadaPorNombre).forEach(([clave, valor]) => {
    if(abuscar == `${clave}`){
      variable = `${valor}`
    }
    //variable += `${clave} = ${valor} ,`;
  });
  return variable;
};
campos.forEach((campo) => {
  const variable = BuscaValor(campo.getAttribute("v-model"));

  valores.push({
    id_ConfigForm: idConfigForm,
    Campo: campo.getAttribute("v-model"),
    valor: variable,
    cadenaFormateada: variable.trim(),
    tipo: campo.getAttribute("type")
  });
});
        ////////////////////////////
        ////////////////////////////
        ////////////////////////////
        //////

        ///////
        console.log("aca valores");
        console.log(valores);
        var variable = "";
        var variable_valor = "";
        var valor_sql = "";
        var v = "";
        for (var i = 0; i < valores.length; i++) {
          if( i > 0){
          variable = valores[i].Campo;
          if((valores[i].tipo == "text")|| (valores[i].tipo == "date")|| (valores[i].tipo == ""))
           v = "'"+ valores[i].valor.replace(",", ".").trim() +"'";
           else
           {
           v = valores[i].valor;//v= v.replace(",", ".");
          }
          valor_sql = valor_sql + variable +" = "+ v +" , ";  
                 
        }
      }
        //var pvariable = variable + ", usuario";
        //var pvariable_valor = variable_valor + ","+this.idUsuario;
        const nuevoValor = valor_sql.trim().substring(0, valor_sql.trim().length - 1);
        console.log(nuevoValor);
        console.log(primero);
        //console.log(pvariable.slice(1));
        //console.log(pvariable_valor );  
    ///////////////////////////////////////////////
    await this.axios.put(`/api/ConfigForm/ModificarTabla/${this.$route.params.idConfigForm}/${this.nuevoValor}/${this.primero}}`)
          .then(datos => {
            this.mostrarAlertaEliminar = false;
            this.mensajeAlertaSuceso = "Los datos se modificaron correctamente";
            this.mostrarAlertaSuceso = true;
            //this.fetch();
  
            setTimeout(() => {
                     this.mostrarAlertaSuceso = false;
                  }, 5000);
          });
    /////////FIN/////////////////////////
    },
async guardarEdicionOriginal() {



if (this.datosDeLaFila) {
  const ediciones = [];
  for (const campoNombre in this.filaEditadaPorNombre) {
    const campo = this.datosDeLaFila.find(item => item.nombre === campoNombre);
    
    if (campo) {
      const id_Answer = campo.id_Answer;
      ediciones.push({
      id_Answer: id_Answer,
      valor: this.filaEditadaPorNombre[campo.nombre].toString()
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
      //this.$emit('edicion-guardada');
      this.mostrarAlertaEliminar = false;
      this.mensajeAlertaSuceso = "Se Grabaron Correctamente los datos";
      this.mostrarAlertaSuceso = true;
      //this.fetch();

      setTimeout(() => {
               this.mostrarAlertaSuceso = false;
            }, 5000);
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

width: 100%;
}
.modal-dialog {


width: 100%;
}
.modal-content{

background: hsl(180, 20%, 99%);
width: 100%;
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