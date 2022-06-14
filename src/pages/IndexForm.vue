<template>
  <q-page padding>
    <h4>Form</h4>
    <q-form
      class="row q-col-gutter-md"
      @submit.prevent="onSubmit"
      @reset="onReset"
      ref="myForm"
    >
      <div class="col-12 col-sm-6">
        <q-input
          label="Producto"
          v-model="product"
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor escriba algo',
          ]"
          lazy-rules
        />
      </div>
      <div class="col-6">
        <q-select
          label="Prioridad"
          v-model="selection"
          :options="options"
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor escriba algo',
          ]"
          lazy-rules
        />
      </div>
      <div class="col-12 col-sm-6">
        <q-toggle label="Acepto los terminos y condiciones" v-model="terms" />
      </div>
      <div class="col-12">
        <q-btn label="submit" color="primary" class="q-mr-sm" type="submit" />
        <q-btn label="reset" color="secondary" outline type="reset" />
      </div>
    </q-form>
    <products-table :products="products" />
  </q-page>
</template>

<script>
import { ref } from "vue";
import { useQuasar } from "quasar";
import ProductsTable from "src/components/ProductsTable.vue";

export default {
  components: { ProductsTable },
  setup() {
    const $q = useQuasar();
    const product = ref(null);
    const selection = ref(null);
    const terms = ref(false);
    const myForm = ref(null);
    const options = ["Máxima", "Moderada", "Mínima"];
    const products = ref([]);
    const onSubmit = () => {
      if (terms.value !== false) {
        $q.notify({
          color: "green-4",
          textColor: "white",
          icon: "cloud_done",
          message: "Guardado",
        });
        myForm.value.resetValidation();
        products.value = [
          ...products.value,
          { product: product.value, priority: selection.value },
        ];
        onReset();
      } else {
        $q.notify({
          color: "red-5",
          textColor: "white",
          icon: "warning",
          message: "Por favor, acepte los términos y condiciones",
        });
      }
    };
    const onReset = () => {
      product.value = null;
      selection.value = null;
      terms.value = false;
    };
    return {
      product,
      selection,
      options,
      onSubmit,
      onReset,
      terms,
      myForm,
      products,
    };
  },
};
</script>
