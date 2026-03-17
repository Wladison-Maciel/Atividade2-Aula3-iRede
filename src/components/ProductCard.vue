<template>
  <div class="product-card">
    <h3>{{ product.name }}</h3>
    <p>Categoria: {{ product.category.name }}</p>
    <p>Preço: R$ {{ product.price }}</p>

    <button @click="handleAdd">
      Adicionar
    </button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import type { Product } from "../interfaces/Product"

export default defineComponent({
  name: "ProductCard",

  props: {
    product: {
      type: Object as () => Product,
      required: true
    }
  },

  emits: ["add-to-cart"],

  methods: {
    handleAdd() {
      this.$emit("add-to-cart", this.product)
    }
  }
})
</script>

<style scoped>
.product-card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
  width: 200px;
}
</style>