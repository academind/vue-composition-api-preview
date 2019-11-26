<template>
  <form id="product-form" @submit="saveProduct">
    <div class="form-control">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="titleInput" />
    </div>
    <div class="form-control">
      <label for="price">Price</label>
      <input type="number" min="0" id="price" step="0.01" v-model="priceInput" />
    </div>
    <button type="submit" :disabled="!isValid">Save</button>
  </form>
</template>

<script>
export default {
  props: {
    createProduct: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      titleInput: '',
      priceInput: '',
      submitted: false
    };
  },
  computed: {
    price() {
      return parseFloat(this.priceInput);
    },
    isValid() {
      let isValid = true;

      if (this.titleInput.trim().length === 0) {
        isValid = false;
      }
      if (isNaN(this.price) || this.price <= 0) {
        isValid = false;
      }
      return isValid;
    }
  },
  watch: {
    formSubmitted() {
      if (this.submitted) {
        this.titleInput = '';
        this.priceInput = '';
        this.submitted = false;
      }
    }
  },
  methods: {
    saveProduct(event) {
      event.preventDefault();
      this.createProduct(this.titleInput, this.price);
      this.submitted = true;
    }
  }
};
</script>

<style scoped>
#product-form {
  width: 90%;
  max-width: 40rem;
  margin: 2rem auto;
  border: 1px solid #ccc;
  padding: 1rem;
}
.form-control {
  margin: 0.5rem 0;
}

label,
input {
  display: block;
  width: 100%;
}

label {
  font-weight: bold;
}

input {
  font: inherit;
  font-size: 1.15rem;
  padding: 0.1rem 0.2rem;
  color: #4d4d4d;
  border: 1px solid #ccc;
}

input:focus {
  outline: none;
  background: #eeeeee;
}

button {
  cursor: pointer;
  font: inherit;
  padding: 0.5rem 2rem;
  background: #440055;
  border: 1px solid #440055;
  color: white;
}

button:focus {
  outline: none;
}

button:hover,
button:active {
  background: #770594;
  border-color: #770594;
}
</style>