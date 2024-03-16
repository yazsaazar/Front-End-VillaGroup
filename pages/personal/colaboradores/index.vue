<template>
  <AdminTemplate :page="page" :modulo="modulo">
    <div slot="body">
      <div class="row justify-content-end">
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
                    <th class="text-muted">Numero de colaborador</th>
                    <th class="text-muted">Nombre</th>
                    <th class="text-muted">Apellidos</th>
                    <th class="text-muted">Puesto</th>
                    <th class="text-muted">Área</th>
                    <th class="text-muted">Resort</th>
                    <th class="text-muted">Estado</th>
                    <th class="text-muted">Acciones</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(m, i) in list" :key="i">
                    <td>{{ m.numero_colaborador }}</td>
                    <td>{{ m.nombre }}</td>
                    <td>{{ m.apellidos }}</td>
                    <td>{{ m.puesto }}</td>
                    <td>{{ m.area.nombre }}</td>
                    <td>{{ m.resort.nombre }}</td>
                    <td style="display: flex; justify-content: center;">
                      <div :style="{ backgroundColor: m.estado === 'habilitado' ? '#68B028' : '#DF4429', borderRadius: '50%', width: '20px', height: '20px' }"></div>
                    </td>
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
      apiUrl: 'colaboradores',
      page: 'Personal',
      modulo: 'Colaboradores',
      url_nuevo: '/personal/colaboradores/nuevo',
      url_editar: '/personal/colaboradores/editar/',
    };
  },
  methods: {
    async GET_DATA(path) {
      try {
        const res = await this.$api.$get(path);
        return res;
      } catch (error) {
        console.error(error);
      }
    },
    async EliminarItem(id) {
  try {
    const res = await this.$api.$delete(`${this.apiUrl}/${id}`);
    console.log(res);
    await this.GET_DATA(this.apiUrl);
    // Después de eliminar, actualizamos la lista para reflejar los cambios
    this.list = this.list.filter(item => item.id !== id);
  } catch (error) {
    console.error(error);
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

.btn-detalles {
  background-color: #b7ac37;
  border: none;
}

</style>
