<template lang="pug">
section
  
  b-table(
    :data="dataProducts",
    ref="table",
    :paginated="isPaginated",
    per-page="5",
    pagination-rounded="true",
    sort-icon="arrow-up",
    default-sort="id",
    aria-next-label="Siguiente",
    aria-previous-label="Anterior",
    aria-page-label="Página",
    aria-current-label="Página actual",
    page-input="false"
  )
    b-table-column(field="sku", label="sku", v-slot="props")
      | {{ props.row.sku }}
    b-table-column(
      field="name",
      sortable,
      numeric,
      label="Título",
      v-slot="props"
    )
      | {{ props.row.name }}
    b-table-column(
      field="quantity",
      sortable,
      numeric,
      label="Creada",
      v-slot="props"
    )
      | {{ props.row.quantity }}
    b-table-column(
      field="price",
      sortable,
      numeric,
      label="Actualizada",
      v-slot="props"
    )
      | {{ props.row.price }}

   
</template>

<script>
export default {
  name: "form-element",
  props: {
    dataProducts: {
      type: Array,
      required: true,
      default: [],
    },
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
