<template lang="pug">
form
  .modal-card
    header.modal-card-head
      p.modal-card-title Creando producto
      button.delete(type="button", @click="$emit('close')")
    section.modal-card-body
      ProductsForm( :data="newElement" ref="formdocument" @createElement="createElement")
    footer.modal-card-foot.is-flex.is-justify-content-end
      b-button(label="Cerrar", @click="$emit('close')")
      b-button(label="Crear", type="is-primary", @click="verifyData")
</template>

<script>
export default {
  name: "creation-element",

  data() {
    return {
      newElement: {
        sku: undefined,
        name: undefined,
        price: undefined,
        quantity: undefined,
      },
      blockForm: false,
    };
  },

  methods: {
    verifyData: function (newElement) {
        console.log(this.$refs)
        this.$refs.formdocument.createElement()
    },
    createElement: function (newElement) {
     
      //Creating element in API
      //send data
      //return new element
      this.$emit("addelement", newElement);
    },
  },
};
</script>
<style scoped>
</style>
