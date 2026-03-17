<template>

  <div>

    <h1>🛒 E-commerce</h1>

    <h2>Produtos</h2>

    <div class="products">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
        @add-to-cart="addToCart"
      />
    </div>

    <hr />

    <h2>Carrinho</h2>

    <p>Total de itens: {{ totalItems }}</p>
    <p>Preço final: R$ {{ finalPrice }}</p>

  </div>

</template>

<script lang="ts">
import { defineComponent } from "vue"
import ProductCard from "./components/ProductCard.vue"

import type { Product } from "./interfaces/Product"
import type { CartItem } from "./interfaces/CartItem"

export default defineComponent({

  components: {
    ProductCard
  },

  data() {
    return {

      products: [
        {
          id: 1,
          name: "Notebook",
          price: 3500,
          category: {
            id: 1,
            name: "Eletrônicos"
          } 
        },
        {
          id: 2,
          name: "Mouse",
          price: 150,
          category: {
            id: 1,
            name: "Eletrônicos"
          }
        },
        {
          id: 3,
          name: "Teclado",
          price: 300,
          category: {
            id: 1,
            name: "Eletrônicos"
          }
        }

      ] as Product[],

      cartItems: [] as CartItem[]

    }
  },

  computed: {

    totalItems(): number {
      return this.cartItems.reduce((total, item) => {
        return total + item.quantity
      }, 0)
    },

    finalPrice(): number {
      return this.cartItems.reduce((total, item) => {
        return total + item.product.price * item.quantity
      }, 0)
    }

  },

  methods: {

    addToCart(product: Product) {

      const existingItem = this.cartItems.find(
        item => item.product.id === product.id
      )

      if (existingItem) {
        existingItem.quantity++
      } else {

        this.cartItems.push({
          product,
          quantity: 1
        })

      }

    }

  }

})
</script>

<style>

.products {
  display: flex;
}

</style>