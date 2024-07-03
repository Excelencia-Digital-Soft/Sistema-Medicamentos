<template>
    <barra-navegacion></barra-navegacion>
    <EditarFilaModalN />
     <!-- Componente que busca medicmanentos de AlfABeta  -->    
     <BuscarMed />
    
    </template>
    <script>
    import EditarFilaModalN from '../components/EditarFilaModalN.vue';
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
        EditarFilaModalN,
        AlertaSuceso,
        'spinner': Spinner,
    
    },
    data() {
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