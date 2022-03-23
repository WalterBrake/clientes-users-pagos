<template lang="pug">
section.section.pt-5.templates
  b-modal(
    v-model="isComponentModalActive",
    has-modal-card="",
    trap-focus="",
    :destroy-on-hide="false",
    aria-role="dialog",
    aria-label="Example Modal",
    close-button-aria-label="Close",
    aria-modal=""
  )
    Modal(@close="isComponentModalActive = false", v-on:addelement="addElement")
  b-modal(
    v-model="isComponentModalPaymentActive",
    has-modal-card="",
    trap-focus="",
    :destroy-on-hide="false",
    aria-role="dialog",
    aria-label="Example Modal",
    close-button-aria-label="Close",
    aria-modal=""
  )
    Payment(@close="isComponentModalActive = false", v-on:addelement="addElement")

  .columns.is-mobile.is-full.pb-3
    .column
      .container
        p.is-size-4 Ordenes de compra

      section
        b-table(
          :data="orders",
          ref="table",
          paginated="",
          per-page="5",
          :opened-detailed="openedElementsArray",
          detailed="",
          detail-key="id",
          :detail-transition="'fade'",
          aria-next-label="Next page",
          aria-previous-label="Previous page",
          aria-page-label="Page",
          aria-current-label="Current page"
        )
          b-table-column(field="id", label="Id", v-slot="props")
            | {{ props.row.id }}
          b-table-column(field="Number", label="number", v-slot="props")
            | {{ props.row.number }}
          b-table-column(field="currency", label="currency", v-slot="props")
            | {{ props.row.currency }}
          b-table-column(field="status", label="status", v-slot="props")
            | {{ props.row.status.financial }}

          template(#detail="props")
            Products(:dataProducts="props.row.items")
            .container.mt-5
              .is-align-items-center.is-flex.is-justify-content-end
                b-button(
                  type="is-primary is-small",
                  @click="isComponentModalActive = true; elementIdSelected = props.row.id"
                ) Añadir elemento
                b-button(
                  type="is-info is-small ml-5  ",
                  @click="isComponentModalPaymentActive = true"
                ) Pagar orden
</template>

<script>
export default {
  name: "plantillas",
  async asyncData({ $axios }) {
    console.log($axios.defaults.headers.common);

    const request = await $axios.$get(
      "https://eshop-deve.herokuapp.com/api/v2/orders"
    );
    console.log(request);
    return { orders: request.orders };
  },
  data() {
    return {
      elementIdSelected: undefined,
      isComponentModalActive: false,
      isComponentModalPaymentActive: false,
      openedElementsArray: [1],
    };
  },
  methods: {
    addElement: function (elementTemplate) {
      for (let o in this.orders) {
        if (this.orders[o].id === this.elementIdSelected) {
          this.orders[o].items.push(elementTemplate);
        }
      }

      this.isComponentModalActive = false;
    },
  },
};
</script>

<style >
.b-table .table {
      background-color: #e5f5ff;

}
</style>