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

                  <div class="form-group col-2">
                    <label for="">numero colaborador</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.numero_colaborador"
                      class="form-control"
                      id=""
                    />
                  </div>


                  <div class="form-group col-5">
                    <label for="">Nombre</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.nombre"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-5">
                    <label for="">apellidos</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.apellidos"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">puesto</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.puesto"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">area</label>
                      <select name="" id="" class="form-control" v-model="model.id_area">
                        <option v-for="m in areas" :value="m.id">{{m.nombre}}</option>
                      </select>
                  </div>

                  <div class="form-group col-4">
                    <label for="">resort</label>
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
        numero_colaborador:"",
        nombre: "",
        apellidos:"",
        puesto:"",
        id_area:"",
        id_resort:"",
        estado:"habilitado"
      },
      apiUrl:'colaboradores',
      page:'Personal',
      modulo:'Colaboradores',
      areas:[],
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
        await Promise.all([this.GET_DATA("areas"), this.GET_DATA("resorts")]).then((v) => {
          this.areas = v[0];
          this.resorts = v[1];
          if(this.areas.length){
              this.model.id_area = this.areas[0].id
          }

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
