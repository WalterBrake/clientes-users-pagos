<template lang="pug">
form
  .modal-card
    section.modal-card-body.is-align-items-center.is-flex.is-justify-content-center.is-flex-direction-column.py-6
      img(src='~assets/sucess-payment.webp' class="column is-7" alt='Buefy', height='28')
      p.is-size-2.has-text-centered.has-text-success Pago exitoso
      p.has-text-grey.is-size-5 Tú pago ya fue procesado
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
