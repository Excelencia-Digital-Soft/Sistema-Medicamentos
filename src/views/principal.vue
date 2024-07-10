<template>
<barra-navegacion></barra-navegacion>
<MostrarCampos />
<br><br>
 <!-- Componente que busca medicmanentos de AlfABeta  -->    
 <BuscarMed />

</template>
<script>
import MostrarCampos from '../components/MostrarCampos.vue';
import BarraNavegacion from '@/components/BarraNavegacion.vue';
import BuscarMed from '../components/BuscarMed.vue';
import grilla from '../components/grilla.vue';
import ListarMed from '../components/ListarMed.vue';
import AlertaSuceso from '../components/AlertaSuceso.vue';
import Spinner from '@/components/Spinner.vue';
export default {

   
name: 'ManagerGrillaView',
components: {
    
    'barra-navegacion': BarraNavegacion,
    
    BuscarMed,
    ListarMed,
    grilla,
    MostrarCampos,
    AlertaSuceso,
    'spinner': Spinner,

},
data() {
    return {
  

};
},
computed: {
},
mounted() {
      
     
  },
  created() {
},
    watch: {
   
  },
  methods: {
  
}
};

</script>