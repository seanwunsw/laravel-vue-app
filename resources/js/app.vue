<template>
    <div>
      <button class="btn btn-success" @click="toggleView">{{ showAddForm ? 'Back to Products' : 'Add Product' }}</button>
      <div v-if="showAddForm">
        <add-product @close="showAddForm = false" @product-added="fetchProducts"></add-product>
      </div>
      <div v-else>
        <product-list @delete-product="deleteProduct" @modify-product="modifyProduct"></product-list>
      </div>
    </div>
  </template>
  
  <script>
  import ProductList from './components/Items.vue';
  import AddProduct from './components/AddProduct.vue';
  
  export default {
    components: {
      ProductList,
      AddProduct,
    },
    data() {
      return {
        showAddForm: false,
      };
    },
    methods: {
        toggleView() {
      this.showAddForm = !this.showAddForm;
    },
      fetchProducts() {
        this.$refs.productList.fetchProducts();
      },
      deleteProduct(productId) {
        this.$refs.productList.deleteProduct(productId);
      },
    },
  };
  </script>
  