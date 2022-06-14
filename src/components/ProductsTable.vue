<template>
  <q-table
    class="q-mt-md"
    title="Productos"
    :columns="columns"
    :rows="products"
    no-data-label="Sin productos para mostrar"
  />
</template>

<script>
const columns = [
  {
    name: "product",
    label: "Producto",
    align: "left",
    field: "product",
    sortable: true,
  },
  {
    name: "priority",
    label: "Prioridad",
    align: "left",
    field: "priority",
    sortable: true,
  },
];
export default {
  props: {
    products: Array,
  },
  setup() {
    return {
      columns,
    };
  },
};
</script>
