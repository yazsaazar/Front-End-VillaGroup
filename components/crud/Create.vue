<template>
  <div class="row">
    <div class="col-12">
      <slot name="body"> </slot>
    </div>


    <div class="col-12">
      <div class="row">
        <div class="col-12">
          <button class="btn btn-villagroupamarillo  text-white w-20 " @click="$router.back()">Regresar</button>

          <button class="btn btn-villagroup text-white w-20" @click="Save()">Guardar</button>
        </div>
      </div>
    </div>



  </div>
</template>

<script>
export default {
  props: {
    model: {
      type: Object,
      default: () => {}
    },
    apiUrl: {
      type: String,
      default: '',
    },
  },

  methods: {
    async Save() {
      try {
        const res = await this.$api.$post(this.apiUrl, this.model);
        console.log(res);
        this.$swal
          .fire({
            title: "Guardado",
            showDenyButton: false,
            showCancelButton: false,
            confirmButtonText: "ok",
          })
          .then((result) => {
            /* Read more about isConfirmed, isDenied below */
            if (result.isConfirmed) {
              this.$router.back();
            }
          });
      } catch (e) {
        console.log(e);
      }
    },
  },
  mounted() {
    this.$nextTick(async () => {
      try {
      } catch (e) {
        console.log(e);
      }
    });
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
