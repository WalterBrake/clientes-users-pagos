<template lang="pug">
div( v-if="$v")
  h1.my-5.is-size-3 Creación de cliente
  b-field(
    label="Monto", v-if="$v.monto"
    :type="$v.monto.$error ? 'is-danger' : ''",
    :message="$v.monto.$error ? 'Obligatorio' : ''"
  )
    b-input(v-model="monto")
 

  .container.mt-5
    .is-align-items-center.is-flex.is-justify-content-end
      b-button(
        type="is-primary is-small",
        @click="createClient()"
      ) Crear


</template>

<script>
import { validationMixin } from "vuelidate";
import { required, decimal } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],

  name: "form-element",

  data() {
    return {
      monto: undefined,
    };
  },

  validations: {
    monto: { required, decimal },
  },
  methods: {
    createClient: async function (newElement) {
      this.blockForm = true;
      this.$v.$reset();
      this.$v.$touch();
      if (this.$v.$anyError) {
        this.blockForm = false;

        this.$buefy.toast.open({
          duration: 5000,
          message: "Por favor, llene los campos correctamente",
          position: "is-top",
          type: "is-primary",
        });

        return;
      }

      const request = await this.$axios.$post(
        "http://localhost:4000/api/payments",
        {
          userId: this.$route.params.user,
          monto: this.monto,
        }
      );

      if (request.code == 1000) {
        this.$router.push(`/`);
      }
    },
  },
};
</script>
<style scoped>
.handler-item {
  cursor: move;
}
.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
</style>
