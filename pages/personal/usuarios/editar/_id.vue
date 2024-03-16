<template>
  <AdminTemplate :page="page" :modulo="modulo">
    <div slot="body">
      <div class="row justify-content-center">
        <div class="col-sm-11 col-12">
          <div class="card">
            <div class="card-header">
              <h3>Actualizar</h3>
            </div>
            <div class="card-body">
              <CrudUpdate :model="model" :apiUrl="apiUrl">
                <div slot="body" class="row">
                  <div class="form-group col-3">
                    <label for="">Usuario</label>
                    <input
                      type="text"
                      v-model="model.usuario"
                      class="form-control"
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Nueva Contraseña</label>
                    <input
                      type="password"
                      v-model="newPassword"
                      class="form-control"
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Resort</label>
                    <select class="form-control" v-model="model.id_resort">
                      <option v-for="m in resorts" :value="m.id" :key="m.id">{{m.nombre}}</option>
                    </select>
                  </div>
                </div>
              </CrudUpdate>
            </div>
          </div>
        </div>
      </div>
    </div>
  </AdminTemplate>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      model: {
        usuario: "",
        id_resort: "",
        password: ""
      },
      newPassword: "", // Agregar nueva propiedad para la nueva contraseña
      apiUrl: 'usuarios',
      page: 'Personal',
      modulo: 'Usuarios',
      resorts: []
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
    async updateModel() {
      try {
        // Actualizar el modelo con la nueva contraseña
        this.model.password = this.newPassword;

        // Enviar la solicitud de actualización al backend
        await this.$api.$put(this.apiUrl + '/' + this.$route.params.id, this.model);

        // Notificar al usuario de la actualización exitosa
        alert('Usuario actualizado exitosamente');
      } catch (error) {
        console.error(error);
        alert('Error al actualizar el usuario');
      }
    }
  },
  mounted() {
    this.$nextTick(async () => {
      try {
        // Obtener datos del usuario y resorts
        const [userData, resortsData] = await Promise.all([
          this.GET_DATA(this.apiUrl + '/' + this.$route.params.id),
          this.GET_DATA('resorts')
        ]);

        // Actualizar el modelo y resorts con los datos obtenidos
        this.model = userData;
        this.resorts = resortsData;

        // Establecer el primer resort como seleccionado por defecto
        if (this.resorts.length) {
          this.model.id_resort = this.resorts[0].id;
        }
      } catch (error) {
        console.error(error);
      }
    });
  }
};
</script>
