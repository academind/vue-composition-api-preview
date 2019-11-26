<template>
  <div id="app">
    <ProductForm :createProduct="createProduct" />
    <Products :items="products" :remove="deleteProduct" />
  </div>
</template>

<script>
import ProductForm from './components/ProductForm.vue';
import Products from './components/Products.vue';

export default {
  name: 'app',
  components: {
    ProductForm,
    Products
  },
  data() {
    return {
      products: []
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
    }
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
</style>
