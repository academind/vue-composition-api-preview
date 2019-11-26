<template>
  <div id="app">
    <div id="user-info">
      <button @click="toggle">{{ show ? 'Hide' : 'Show'}} User Details</button>
      <p v-if="show">You're logged in!</p>
    </div>
    <ProductForm :createProduct="createProduct" />
    <Products :items="products" :remove="deleteProduct" />
  </div>
</template>

<script>
import ProductForm from './components/ProductForm.vue';
import Products from './components/Products.vue';
import { toggleMixin } from './mixins/toggle';

export default {
  name: 'app',
  components: {
    ProductForm,
    Products
  },
  mixins: [toggleMixin],
  data() {
    return {
      products: [],
      // showUserInfo: false
    };
  },
  methods: {
    createProduct(title, price) {
      const newProduct = {
        id: Math.random(),
        title: title,
        price: price
      };

      this.products.push(newProduct);
    },
    deleteProduct(productId) {
      this.products = this.products.filter(p => p.id !== productId);
    },
    // toggleUserInfo() {
    //   this.showUserInfo = !this.showUserInfo;
    // }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

#user-info {
  margin: 2rem auto;
  width: 90%;
  max-width: 40rem;
}
</style>
