<template>
  <div>
    <header class="top-bar spread">
        <nav class="top-bar-nav">
          <router-link to="/" class="top-bar-link">
            <i class="icofont-spoon-and-fork"></i>
            <span>Home</span>
          </router-link>
          <router-link to="/products" class="top-bar-link">
            <span>Products</span>
          </router-link>
          <router-link to="/past-orders" class="top-bar-link">
            <span>Past Orders</span>
          </router-link>
        </nav>
        <div class="top-bar-cart-link" @click="toggleSidebar">
          <i class="icofont-cart-alt icofont-1x"></i>
          <span>Cart ({{ totalQuantity }})</span>
        </div>
    </header>
    <router-view :inventory="inventory" :addToCart="addToCart" />
    <Sidebar
      v-if="showSidebar"
      :toggle="toggleSidebar"
      :cart="cart"
      :inventory="inventory"
      :remove="removeItem"
    />
  </div>
</template>

<script>
import Sidebar from '@/components/Sidebar.vue'
import food from './food.json'

export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: true,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => acc + curr, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
      console.log(this.cart)
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>

<style scoped>
h1 {
  color: blue
}
</style>
