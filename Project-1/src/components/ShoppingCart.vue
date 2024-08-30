<template>
  <div>
    <h2>Shopping Cart</h2>

    <!-- Display total items in the cart -->
    <h3>Total Items in Cart: {{ totalItems }}</h3>

    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Price($)</th>
          <th>Category</th>
          <th>Title</th>
          <th>Image</th>
          <th>Rating</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.category }}</td>
          <td>{{ product.title }}</td>
          <td><img :src="product.image" alt="Product Image" style="width: 150px; height: 150px;" /></td>
          <td>{{ product.rating.rate }}</td>
          <td>
            <button @click="addToCart(product)">+</button>
            <button @click="removeFromCart(product)">-</button>
          </td>
        </tr>
      </tbody>
    </table>

    <h3>Cart</h3>
    <div v-if="cart.length > 0">
      <ul>
        <li v-for="item in cart" :key="item.product.id">
          {{ item.product.title }} - Quantity: {{ item.quantity }}
        </li>
      </ul>
    </div>
    <div v-else>
      <p>Your cart is empty</p>
    </div>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue';

export default {
  setup() {
    const products = ref([]);
    const cart = ref([]);

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

    const addToCart = (product) => {
      const cartItem = cart.value.find((item) => item.product.id === product.id);
      if (cartItem) {
        cartItem.quantity += 1;
      } else {
        cart.value.push({ product, quantity: 1 });
      }
    };

    const removeFromCart = (product) => {
      const cartItem = cart.value.find((item) => item.product.id === product.id);
      if (cartItem) {
        cartItem.quantity -= 1;
        if (cartItem.quantity === 0) {
          cart.value = cart.value.filter((item) => item.product.id !== product.id);
        }
      }
    };

    // Compute total items in the cart
    const totalItems = computed(() => {
      return cart.value.reduce((total, item) => total + item.quantity, 0);
    });

    onMounted(() => {
      fetchProducts();
    });

    return {
      products,
      cart,
      totalItems,
      addToCart,
      removeFromCart,
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
