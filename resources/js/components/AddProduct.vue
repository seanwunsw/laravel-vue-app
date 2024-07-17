<template>
    <div>
      <h2>Add Product</h2>
      <form @submit.prevent="addProduct">
        <div class="form-group">
          <label for="name">Name:</label>
          <input type="text" class="form-control" v-model="product.name">
        </div>
        <div class="form-group">
          <label for="qty">Qty:</label>
          <input type="number" class="form-control" v-model="product.qty">
        </div>
        <div class="form-group">
          <label for="desc">Desc:</label>
          <textarea class="form-control" id="desc" rows="3" v-model="product.desc"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">Add Product</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        product: {
          name: '',
          qty: '',
          desc: '',
        },
      };
    },
    methods: {
      async addProduct() {
        await window.axios.post(`/products`, this.product);
        this.$emit('close');
      },
    },
  };
  </script>
  <style>
  form {
    min-width:300px;
    max-width:400px;
    padding:20px;
    margin:0 auto;
  }
  </style>