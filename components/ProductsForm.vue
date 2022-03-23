<template lang="pug">
div
  b-field(
    label="SKU",
    :type="v$.data.sku.$error ? 'is-danger' : ''",
    :message="v$.data.sku.$error ? 'Obligatorio' : ''"
  )
    b-input(v-model="v$.data.sku.$model")
  b-field(
    label="Descripción",
    :type="v$.data.name.$error ? 'is-danger' : ''",
    :message="v$.data.name.$error ? 'Obligatorio' : ''"
  )
    b-input(maxlength="200", type="textarea", v-model="v$.data.name.$model")
  b-field(
    label="Precio",
    :type="v$.data.price.$error ? 'is-danger' : ''",
    :message="v$.data.price.$error ? 'Obligatorio' : ''"
  )
    b-input(
      v-model="v$.data.price.$model",
      type="number",
      placeholder="0",
      min="0"
    )
  b-field(
    label="Cantidad",
    :type="v$.data.quantity.$error ? 'is-danger' : ''",
    :message="v$.data.quantity.$error ? 'Obligatorio' : ''"
  )
    b-input(
      v-model="v$.data.quantity.$model",
      type="number",
      placeholder="0",
      min="0"
    )
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, between } from "@vuelidate/validators";

export default {
  setup() {
    return { v$: useVuelidate() };
  },
  name: "form-element",
  props: {
    data: {
      type: Object,
      required: true,
      default: {
        sku: undefined,
        name: undefined,
        price: undefined,
        quantity: undefined,
      },
    },
  },
  validations: {
    data: {
      sku: { required },
      name: { required },
      price: { required },
      quantity: { required },
    },
  },
  mounted() {
    console.log(this.v$);
  },
  methods: {
    createElement: async function (newElement) {
      const isFormCorrect = await this.v$.$validate();
      // you can show some extra alert to the user or just leave the each field to show it's `$errors`.
      if (!isFormCorrect) {
        this.$buefy.toast.open({
          duration: 5000,
          message: "Por favor, llene los campos correctamente",
          position: "is-top",
          type: "is-primary",
        });
        return;
      }

      this.$emit("createElement", this.data);

      this.data={
        sku: undefined,
        name: undefined,
        price: undefined,
        quantity: undefined,
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
