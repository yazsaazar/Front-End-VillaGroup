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
                    <label for="">Resort</label>
                    <select name="" id="" class="form-control" v-model="model.id_resort">
                      <option v-for="m in resorts" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                  <div class="form-group col-3">
                    <label for="">Fecha compra</label>
                    <input
                      type="date"
                      name=""
                      v-model="model.fecha_compra"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Marca</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.marca"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Modelo</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.modelo"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Numero serie</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.numero_serie"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Tipo</label>
                    <select name="" id="" class="form-control" v-model="model.id_tipo">
                      <option v-for="m in tipos" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                  <div class="form-group col-3">
                    <label for="">Especificaciones</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.especificaciones"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Garantia</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.garantia"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Etiqueta</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.etiqueta"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-3">
                    <label for="">Nota</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.nota"
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
      title: "this.modulo",
    };
  },
  data() {
    return {
      model: {
        id_resort:"",
        fecha_compra:"",
        marca:"",
        modelo: "",
        numero_serie:"",
        id_tipo:"",
        especificaciones:"",
        garantia:"",
        etiqueta:"",
        nota:"",
      },
      apiUrl:'equipos',
      page:'Equipos',
      modulo:'Equipos',
      resorts:[],
      tipos:[],
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
          this.GET_DATA(this.apiUrl+'/'+this.$route.params.id),this.GET_DATA("resorts"),this.GET_DATA("tipos")
        ]).then((v) => {
          this.model = v[0];
          this.resorts = v[1];
          this.tipos = v[2];

          if(this.resorts.length){
              this.model.id_resort = this.resorts[0].id
          }
          if(this.tipos.length){
              this.model.id_tipo = this.tipos[0].id
          }
        });
      } catch (e) {
        console.log(e);
      }
    });
  },
};
</script>
