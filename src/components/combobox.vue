<template>
  <div>
    <h5>Listado de datos cargados</h5>
    
    <v-text-field v-model="searchQuery" label="Buscador" append-inner-icon="mdi-magnify" variant="underlined" size="small" ></v-text-field>
    <table class="table table-bordered table-hover">
      <thead>
        <tr>
          <th v-for="(header, index) in headers" :key="index">{{ header }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, rowIndex) in paginatedRows" :key="rowIndex">
          <td v-for="(header, colIndex) in headers" :key="colIndex">{{ row[header] }}</td>
          <td>
          <v-btn @click="sendRowData(row)" class="bg-primary" >Ver</v-btn>
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
</template>

<script>
export default {
  data() {
    return {
      ListaFormulariosArticulos:'',
      rows: [],
      //rows: [
       // { Nombre: 'Adrian', Edad: 50, Email: 'adrian@example.com' },
       // { Nombre: 'Hugo', Edad: 60, Email: 'hugo@example.com' },
       // { Nombre: 'Luis', Edad: 40, Email: 'luis@example.com' },
       // { Nombre: 'Maria', Edad: 35, Email: 'maria@example.com' },
       // { Nombre: 'Ana', Edad: 28, Email: 'ana@example.com' },
       // { Nombre: 'Jorge', Edad: 45, Email: 'jorge@example.com' },
       // { Nombre: 'Pablo', Edad: 32, Email: 'pablo@example.com' }
      //],
      searchQuery: '',
      currentPage: 1,
      itemsPerPage: 3
    };
  },
  created() {
      this.idUsuario = this.$store.state.id_usuario;
  this.fetchArticulosMed();
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
  },
  methods: {
      
  sendRowData(row) {
    const keys = Object.keys(row);
    //alert(keys[0]); Nombre de la columna
    const entries = Object.entries(row);
    const primerpar = entries[0];  // Valor de la columna
    //alert('Dato de la fila seleccionada:', row);
    console.log('Dato de la fila seleccionada:', primerpar[1]);
    //this.processRow(row);
    
  },

  async fetchArticulosMed() {
      
      //this.MostrarSpinner = true; //abrir spinner mientras realiza la solicitud 
      //const respuesta = await this.axios.get("/api/ConfigForm/ListaField?pTipo=2136")
      const respuesta = await this.axios.get(`/api/ConfigForm/ListarArticulos?pTipo=${this.idUsuario}`)
        .then((respuesta) => {
          //this.ListaFormulariosArticulos = respuesta.data.lista
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
    }
  }
};
</script>

<style scoped>
.table {
  width: 100%;
  border-collapse: collapse;
}
.table th, .table td {
  border: 1px solid #ddd;
  padding: 8px;
}
.table th {
  background-color: #f2f2f2;
  text-align: left;
}
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px 0;
}
.pagination button {
  margin: 0 5px;
}
</style>

