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
                  <div class="form-group col-12">
                    <label for="">Nombre</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.nombre"
                      class="form-control"
                      id=""
                    />
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
  head() {
    return {
      title: this.modulo,
    };
  },
  data() {
    return {
      model: {
        nombre: "",
      },
      apiUrl:'departamentos',
      page:'Ubicación',
      modulo:'Departamentos',
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
        await Promise.all([
          this.GET_DATA(this.apiUrl+'/'+this.$route.params.id),]).then((v) => {
          this.model = v[0];
        });
      } catch (e) {
        console.log(e);
      }
    });
  },
};
</script>
