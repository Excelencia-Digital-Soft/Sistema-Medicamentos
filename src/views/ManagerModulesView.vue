<template>
  <barra-navegacion></barra-navegacion>
  
  <spinner :visible="MostrarSpinner"></spinner>
  
  <div class="container-sm">
  <div v-if="!MostrarSpinner">
    <form @submit.prevent="obtenerValores">
      <div id="ContenedorDeCampos">
        <div class="form-group">
          <div class="card border border-2  mx-auto mb-2 bg-white p-2" style="max-width: 98%; margin-bottom: 1%; margin-top: 1%" >
    
          <div v-for="formulario of daform" :key="formulario.idConfigForm">
            <div class="col p-1 ">
             <b> {{ formulario.titulo }} </b> {{ formulario.descripcion }} 
              
            </div>
          </div>
        </div>
        <div class="card border border-2  mx-auto   shadow-lg mb-2 bg-white p-3" style="max-width: 98%; margin-bottom: 1%; margin-top: 1%" >
    
          <div class="row">
          <div v-for="campos of dafield" :key="campos.id_Field" :class="campos.posi">
            <label class="badge bg-secondary" :for="campos.nombre">{{ campos.etiqueta }}</label>
            <!-- Si el tipo es "select", renderiza un select -->
            <select :v-model="campos.nombre" v-if="campos.tipo === 'select'"   :class="campos.clase"
        :required="campos.requerido" :identificador="campos.id_Field">
        <option value="">Selecciona una opción </option>
        <option v-for="Combo in this[campos.opciones.trim()]" :value="Combo.codigo">{{Combo.nombre}}</option>
      </select> 
            <!--
            <select v-if="campos.tipo === 'select'" :name="campos.nombre" :class="campos.clase"
              :required="campos.requerido" :identificador="campos.id_Field">
              <option v-for="opcion in campos.opciones ? campos.opciones.split(',') : []" :value="opcion.trim()">{{
                opcion.trim() }}</option>
            </select>
            -->
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
            <!-- Si no, renderiza los demas tipos de input -->
            <v-text-field v-else :type="campos.tipo" :placeholder="campos.marcador"  :name="campos.nombre"
              :required="campos.requerido" :identificador="campos.id_Field" variant="underlined"></v-text-field>
          </div>
        </div>
      </div>

        </div>
      </div>
      <div class="row">
        <div class="col-auto">
          <div class="col  p-3 text-center">
            <button type="submit" class="btn btn-success btn-sm">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-floppy-fill"
                viewBox="0 0 16 16">
                <path
                  d="M0 1.5A1.5 1.5 0 0 1 1.5 0H3v5.5A1.5 1.5 0 0 0 4.5 7h7A1.5 1.5 0 0 0 13 5.5V0h.086a1.5 1.5 0 0 1 1.06.44l1.415 1.414A1.5 1.5 0 0 1 16 2.914V14.5a1.5 1.5 0 0 1-1.5 1.5H14v-5.5A1.5 1.5 0 0 0 12.5 9h-9A1.5 1.5 0 0 0 2 10.5V16h-.5A1.5 1.5 0 0 1 0 14.5v-13Z" />
                <path
                  d="M3 16h10v-5.5a.5.5 0 0 0-.5-.5h-9a.5.5 0 0 0-.5.5V16Zm9-16H4v5.5a.5.5 0 0 0 .5.5h7a.5.5 0 0 0 .5-.5V0ZM9 1h2v4H9V1Z" />
              </svg>
              Guardar 24</button>
          </div>
        </div>
        <div class="col-auto">
          <div class="col  p-3 text-center">
            <button type="reset" class="btn btn-secondary btn-sm" @click="cancelar">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                class="bi bi-x-square-fill" viewBox="0 0 16 16">
                <path
                  d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm3.354 4.646L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 1 1 .708-.708z" />
              </svg>
              Cancelar</button>
          </div>
        </div>
      </div>
    </form>
  </div>
</div>
</template>

<script>
import BarraNavegacion from '@/components/BarraNavegacion.vue';
import Spinner from '@/components/Spinner.vue';
export default {
  name: 'ManagerModulesView',
  components: {
    'barra-navegacion': BarraNavegacion,
    'spinner': Spinner
  },
  data: function () {
    return { daform: [], dafield: [], ListaCombos: [],
            ListaCombosI:'',
            ListaCombosII:'', MostrarSpinner: false }
  },
  created() {
    this.fetch();
    this.MostrarCombo();
        this.MostrarComboI();
        this.MostrarComboII();
        this.MostrarComboIII();
  },
  methods: {
    async fetch() {
      this.MostrarSpinner = true;
      const idConfigForm = this.$route.params.idConfigForm;
      await this.axios.get(`/api/ConfigForm/MostrarFormularioCompleto/${idConfigForm}`)
        .then((respuesta) => {
          this.daform = respuesta.data;
          this.dafield = respuesta.data.datosField;
          console.log(this.dafield);
        })
        .catch(err => {
          console.log(err);
        }).finally(() => {
          //finaliza el spinner
          // Ocultamos el spinner luego de finalizar la solicitud
          this.MostrarSpinner = false;
        });
    },
    async MostrarCombo() {
      
      //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2129")
        .then((respuesta) => {
          this.ListaCombos = respuesta.data.lista;
          
          console.log("Lista Combos ListaCombos");
          console.log(this.ListaCombos);
         
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
      const respuesta = await this.axios.get("/api/ConfigForm/ListaCombo?pTipo=1&pId=2131")
        .then((respuesta) => {
          this.ListaCombosI = respuesta.data.lista;
          
          console.log("Lista Combos ListaCombosI");
          console.log(this.ListaCombosI);
         
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
          
          console.log("Lista Combos ListaCombosI");
          console.log(this.ListaCombosII);
         
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
          
          console.log("Lista Combos ListaCombosI");
          console.log(this.ListaCombosII);
         
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

      });
      //enviar valores a la api
      // Realiza una solicitud POST a la API para guardar los registros
      this.axios.post('/api/ConfigForm/Respuestas/Guardar', valores)
        .then((respuesta) => {

          //redirigir a la grilla dinamica
          this.$router.push(`/grilla/${idConfigForm}`);

        })
        .catch(err => {
          console.log('Error al guardar los registros:', err);
        });


    },
    cancelar() {
      // Retrocede en la historia de navegación
      this.$router.go(-1);
    }
  }
};
</script>
