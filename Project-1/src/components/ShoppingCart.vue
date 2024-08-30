<template>
  <div>
    <h2>Shopping Cart</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Price</th>
          <th>Category</th>
          <th>Title</th>
          <th>Image</th>
          <th>Rating</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.category }}</td>
          <td>{{ product.title }}</td>
          <td><img :src="product.image" alt="Product Image" style="width: 50px; height: 50px;" /></td>
          <td>{{ product.rating.rate }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>


 
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const products = ref([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        products.value = await response.json();
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    onMounted(() => {
      fetchProducts();
    });

    return {
      products,
    };
  },
};
</script>

<style scoped>
table, th, td {
  border: 1px solid black;
}
table {
  width: 100%;
}
img {
  object-fit: contain;
}
</style>
