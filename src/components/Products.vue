<template>
  <ul>
    <li v-for="prod of items" :key="prod.id" @click="removeProduct(prod.id)">
      <h2>{{ prod.title }}</h2>
      <h3>Price: ${{ prod.price.toFixed(2) }}</h3>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true
    },
    remove: {
      type: Function,
      required: true
    }
  },
  methods: {
    removeProduct(prodId) {
      this.remove(prodId);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  padding: 0;
  width: 90%;
  max-width: 40rem;
}

li {
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  margin: 1rem 0;
}

li h2 {
  font-size: 1.25rem;
  margin: 0.25rem 0;
}

li h3 {
  font-size: 1rem;
  color: #525252;
  margin: 0;
}
</style>