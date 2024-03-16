<template>


  <AdminTemplate :page="page" :modulo="modulo">
    <div slot="body">
      <div class="row">
        <div class="col-12 mb-3">
          <nuxtLink :to="url_nuevo" class="btn btn-villagroupamarillo btn-sm text-white">
            <i class="fas fa-plus mr-1 text-white"></i> Agregar
          </nuxtLink>
        </div>
        <div class="col-12">
          <div class="card">
            <div class="card-body text-center">
              <table class="table">
                <thead class="thead-light">
                  <tr>
                    <th class="text-muted">Resort</th>
                    <th class="text-muted">Fecha compra</th>
                    <th class="text-muted">Marca</th>
                    <th class="text-muted">Modelo</th>
                    <th class="text-muted">Numero serie</th>
                    <th class="text-muted">Tipo</th>
                    <th class="text-muted">Especificaciones</th>
                    <th class="text-muted">Garantia</th>
                    <th class="text-muted">Etiqueta</th>
                    <th class="text-muted">Nota</th>
                    <th class="text-muted">Acciones</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(m, i) in list">
                    <td>{{ m.resort.nombre }}</td>
                    <td>{{ formatFecha(m.fecha_compra) }}</td>
                    <td>{{ m.marca }}</td>
                    <td>{{ m.modelo }}</td>
                    <td>{{ m.numero_serie }}</td>
                    <td>{{ m.tipo.nombre }}</td>
                    <td>{{ m.especificaciones }}</td>
                    <td>{{ m.garantia }}</td>
                    <td>{{ m.etiqueta }}</td>
                    <td>{{ m.nota }}</td>
                    <td>
                      <div role="group">
                        <nuxtLink :to="url_editar + m.id" class="btn btn-villagroupamarillo btn-sm mr-2">
                          <i class="fas fa-pen fa-2x text-white"></i>
                        </nuxtLink>
                        <button @click="Eliminar(m.id)" class="btn btn-villagroup btn-sm">
                          <i class="fas fa-trash fa-2x text-white"></i>
                        </button>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </AdminTemplate>
</template>

<script>
export default {
  head() {
    return {
      title: this.modulo,
    };

  },

  data() {
    return {
      list: [],
      apiUrl:'equipos',
      page:'Equipos',
      modulo:'Equipos',
      url_nuevo:'/equipos/equipos/nuevo',
      url_editar:'/equipos/equipos/editar/'
    };
  },
  methods: {
    formatFecha(fecha) {
      // Convertir la fecha en un objeto Date
      const dateObj = new Date(fecha);

      // Obtener el día, mes y año
      const dia = dateObj.getDate();
      const mes = dateObj.getMonth() + 1; // El mes es indexado desde 0
      const año = dateObj.getFullYear();

      // Formatear la fecha como "DD/MM/YYYY"
      return `${dia}/${mes}/${año}`;
    },


    async GET_DATA(path) {
      const res = await this.$api.$get(path);
      return res;
    },
    async EliminarItem(id) {
      this.load = true;
      try {
        const res = await this.$api.$delete(this.apiUrl+"/"+id);
        console.log(res);
        await Promise.all([this.GET_DATA(this.apiUrl)]).then((v) => {
          this.list = v[0];
        });
      } catch (e) {
        console.log(e);
      }
    },


    Eliminar(id) {
  this.$swal.fire({
    title: '¿Deseas eliminar el registro?',
    showCancelButton: true,
    confirmButtonText: 'Eliminar',
    cancelButtonText: 'Cancelar',
    icon: 'warning',
    showClass: {
      popup: 'swal2-noanimation',
    },
    hideClass: {
      popup: '',
    },
    iconColor: '#B58A37',
    cancelButtonColor: "#A27C32",
  }).then(async (result) => {
    if (result.isConfirmed) {
      await this.EliminarItem(id);
    }
  });
},



  },
  async mounted() {
    try {
      const data = await this.GET_DATA(this.apiUrl);
      this.list = data;
    } catch (e) {
      console.log(e);
    }
  },
};
</script>

<style scoped>
.btn-villagroupamarillo {
  background-color: #FFB800;
  border: none;
}
.btn-villagroup {
  background-color: #A27C32;
  border: none;
}


</style>

