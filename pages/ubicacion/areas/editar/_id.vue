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
                  <div class="form-group col-8">
                    <label for="">Nombre</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.nombre"
                      class="form-control"
                      id=""
                    />
                  </div>
                  <div class="form-group col-4">
                    <label for="">Departamento</label>
                    <select name="" id="" class="form-control" v-model="model.id_departamento">
                      <option v-for="m in departamentos" :value="m.id">{{m.nombre}}</option>
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
  head() {
    return {
      title: this.modulo,
    };
  },
  data() {
    return {
      model: {
        nombre: "",
        id_departamento:"",
      },
      apiUrl:'areas',
      page:'Ubicación',
      modulo:'Areas',
      departamentos:[]
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
          this.GET_DATA(this.apiUrl+'/'+this.$route.params.id),this.GET_DATA('departamentos')
        ]).then((v) => {
          this.model = v[0];
          this.departamentos = v[1];
          if(this.departamentos.length){
            this.model.id_departamento = this.departamentos[0].id
          }
        });
      } catch (e) {
        console.log(e);
      }
    });
  },
};
</script>
