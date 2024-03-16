<template>
  <AdminTemplate :page="page" :modulo="modulo">
    <div slot="body">
      <div class="row justify-content-center">
        <div class="col-sm-11 col-12">
          <div class="card">
            <div class="card-header">
              <h3>Agregar</h3>
            </div>
            <div class="card-body">
              <CrudCreate :model="model" :apiUrl="apiUrl">
                <div slot="body" class="row">
                  <div class="form-group col-4">
                    <label for="">Usuario</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.usuario"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Contraseña</label>
                    <input
                      type="password"
                      name=""
                      v-model="model.password"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Resort</label>
                    <select name="" id="" class="form-control" v-model="model.id_resort">
                      <option v-for="m in resorts" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                </div>
              </CrudCreate>
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
  head() {
    return {
      title: "this.modulo",
    };
  },
  data() {
    return {
      model: {
        usuario:"",
        id_resort:"",
        password:""
      },
      apiUrl:'register',
      page:'Personal',
      modulo:'Usuarios',
      resorts:[],

    };
  },
  methods: {
    async GET_DATA(path) {
      const res = await this.$api.$get(path);
      return res;
    },
  },
  mounted() {
    this.$nextTick(async () => {
      try {
        await Promise.all([this.GET_DATA("resorts")]).then((v) => {
          this.resorts = v[0];
          if(this.resorts.length){
              this.model.id_resort = this.resorts[0].id
          }

        });
      } catch (e) {
        console.log(e);
      }
    });
  },

};
</script>
