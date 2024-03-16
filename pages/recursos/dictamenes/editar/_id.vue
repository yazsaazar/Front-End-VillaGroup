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


                  <div class="form-group col-4">
                    <label for="">Articulo</label>
                    <select name="" id="" class="form-control" v-model="model.id_tipo">
                      <option v-for="m in tipos" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                  <div class="form-group col-4">
                    <label for="">Equipo</label>
                    <select name="" id="" class="form-control" v-model="model.id_equipo">
                      <option v-for="m in equipos" :value="m.id">{{m.numero_serie}}</option>
                    </select>
                  </div>

                  <div class="form-group col-4">
                    <label for="">Numero inventario</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.numero_inventario"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Ubicacion</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.ubicacion"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Adquisicion</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.adquisicion"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Calificacion</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.calificacion"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Motivo</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.motivo"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Imagen etiqueta</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.img_etiqueta"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Imagen equipo</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.img_equipo"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Documento firmado</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.doc_firma"
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
        id_tipo:"",
        id_equipo: "",
        numero_inventario:"",
        ubicacion:"",
        adquisicion:"",
        calificacion:"",
        motivo:"",
        img_etiqueta:"",
        img_equipo:"",
        doc_firma:""
      },
      apiUrl:'dictamenes',
      page:'Recursos',
      modulo:'Dictamenes',
      tipos:[],
      equipos:[],
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
          this.GET_DATA(this.apiUrl+'/'+this.$route.params.id),this.GET_DATA("tipos"),this.GET_DATA("equipos")
        ]).then((v) => {
          this.model = v[0];

          this.tipos = v[1];
          this.equipos = v[2];

          if(this.tipos.length){
              this.model.id_tipo = this.tipos[0].id
          }

          if(this.equipos.length){
              this.model.id_equipo = this.equipos[0].id
          }
        });
      } catch (e) {
        console.log(e);
      }
    });
  },
};
</script>
