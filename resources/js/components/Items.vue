<template>
  <div v-if="products.length<=0"><h3>There is no product right now! Add some by clicking the button above</h3></div>
  <table v-else class="table table-striped table-dark">
    <thead>
      <tr>
        <th scope="col-3">Name:</th>
        <th scope="col-3">Qty:</th>
        <th scope="col-3">Desc:</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.name }}</td>
        <td>{{ product.qty }}</td>
        <td>{{ product.desc }}</td>
        <td><button class="btn btn-danger" @click="deleteProduct(product.id)">Delete</button></td>
      </tr>
    </tbody>
  </table>


</template>
<script>
export default {
  mounted() {
    console.log('Component mounted.');
    this.fetchProducts();
  },
  methods: {
    async fetchProducts() {
      const res = await window.axios.get(`/products`);
      this.products = res.data;
    },
    async deleteProduct(productid) {
      try {
        console.log('remove button clicked ', productid);
        await window.axios.delete('/products/' + productid);
        console.log('Product deleted successfully');
        this.fetchProducts(); // Refresh the product list
      } catch (error) {
        console.error('Failed to delete product:', error);
      }
    },
  },
  data() {
    return {
      products: [

      ]
    }
  },
}
</script>
<style></style>