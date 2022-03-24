<template lang="pug">
section.section.pt-5.templates
  .columns.is-mobile.is-full.pb-3
    .column
      .container
        p.is-size-4 Clientes

      section
        b-table(
          :data="usersData",
          ref="table",
          paginated="",
          per-page="5",
          :opened-detailed="openedElementsArray",
          detailed="",
          detail-key="userId",
          :detail-transition="'fade'",
          aria-next-label="Next page",
          aria-previous-label="Previous page",
          aria-page-label="Page",
          aria-current-label="Current page"
        )
          b-table-column(field="id", label="ID", v-slot="props")
            | {{ props.row.userId }}
          b-table-column(field="Number", label="Cliente", v-slot="props")
            | {{ `Nombre: ${props.row.name} Teléfono: ${props.row.telephone} Último pago: ${new Date(props.row.lastPayment).toLocaleString('es-MX')}` }}
         

          template(#detail="props")
            p(v-if="props.row.Payments.length==0" class="has-text-centered") No hay pagos
            b-table( 
                v-if="props.row.Payments.length!=0"
                :data="props.row.Payments",
                ref="table",
                :opened-detailed="openedElementsArray",
                
                detail-key="paymentId",
                :detail-transition="'fade'",
                aria-next-label="Next page",
                aria-previous-label="Previous page",
                aria-page-label="Page",
                aria-current-label="Current page"
              )
                b-table-column(field="id", label="ID", v-slot="data")
                  | {{ data.row.paymentId }}
                b-table-column(field="Number", label="Monto", v-slot="data")
                  | {{ `Nombre: ${data.row.monto}` }}
                b-table-column(field="id", label="Fecha y hora", v-slot="data")
                  | {{  new Date(data.row.createdAt).toLocaleString('es-MX')}}

          
            .container.mt-5
              .is-align-items-center.is-flex.is-justify-content-end
                b-button(
                  type="is-primary is-small",
                  @click="addPayment(props.row.userId)"
                ) Añadir pago 
      section
        .container.mt-5
          .is-align-items-center.is-flex.is-justify-content-end
            b-button(
              type="is-primary is-small",
              @click="addClient()"
            ) Añadir cliente
               
</template>

<script>
export default {
  name: "plantillas",
  async asyncData({ $axios }) {
    const request = await $axios.$get("http://localhost:4000/api/users");
    console.log(request);
    return { usersData: request.data };
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
    addClient: function (elementTemplate) {
      this.$router.push(`/agregarCliente`);
    },
    addPayment: function (userId) {
      this.$router.push(`/${userId}/agregarPago`);
    },
  },
};
</script>

<style>
.b-table .table {
  background-color: #e5f5ff;
}
</style>
