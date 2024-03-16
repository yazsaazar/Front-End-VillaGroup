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
                    <label for="">Colaborador</label>
                    <select name="" id="" class="form-control" v-model="model.id_colaborador">
                      <option v-for="m in colaboradores" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                  <div class="form-group col-4">
                    <label for="">Fecha</label>
                    <input
                      type="date"
                      name=""
                      v-model="model.fecha"
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

                  <div class="form-group col-4">
                    <label for="">Area</label>
                    <select name="" id="" class="form-control" v-model="model.id_area">
                      <option v-for="m in areas" :value="m.id">{{m.nombre}}</option>
                    </select>
                  </div>

                  <div class="form-group col-4">
                    <label for="">Puesto</label>
                    <input
                      type="text"
                      name=""
                      v-model="model.puesto"
                      class="form-control"
                      id=""
                    />
                  </div>

                  <div class="form-group col-4">
                    <label for="">Equipo</label>
                    <select name="" id="" class="form-control" v-model="model.id_equipo">
                      <option v-for="m in equipos" :value="m.id">{{m.numero_serie}}</option>
                    </select>
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
      title: this.modulo,
    };
  },
  data() {
    return {
      model: {
        id_colaborador:"",
        fecha:"",
        id_resort: "",
        id_area:"",
        puesto:"",
        id_equipo:"",
        doc_firma:""
      },
      apiUrl:'resguardos',
      page:'Recursos',
      modulo:'Resguardos',
      colaboradores:[],
      resorts:[],
      areas:[],
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
        await Promise.all([this.GET_DATA("colaboradores"),this.GET_DATA("resorts"),this.GET_DATA("areas"),this.GET_DATA("equipos")]).then((v) => {
          this.colaboradores = v[0];
          this.resorts = v[1];
          this.areas = v[2];
          this.equipos = v[3];

          if(this.colaboradores.length){
              this.model.id_colaborador = this.colaboradores[0].id
          }

          if(this.resorts.length){
              this.model.id_resort = this.resorts[0].id
          }

          if(this.areas.length){
              this.model.id_area = this.areas[0].id
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
