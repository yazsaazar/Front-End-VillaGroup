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
                  <th class="text-muted">Nombre</th>
                  <th class="text-muted">Departamentos</th>
                  <th class="text-muted">Acciones</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(m, i) in list" :key="i">
                    <td>{{ m.nombre }}</td>
                    <td>{{ m.departamento.nombre }}</td>
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
      apiUrl:'areas',
      page:'Ubicación',
      modulo:'Areas',
      url_nuevo:'/ubicacion/areas/nuevo',
      url_editar:'/ubicacion/areas/editar/'
    };
  },
  methods: {
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
