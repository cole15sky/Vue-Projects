<template>
  <div>
    <svg
    class="absolute top-6 right-12"
    style="height: 50px; width: 50px;"
      xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512">
      <path d="M0 24C0 10.7 10.7 0 24 0L69.5 0c22 0 41.5 12.8 50.6 32l411 0c26.3 0 45.5 25 38.6 50.4l-41 152.3c-8.5 31.4-37 53.3-69.5 53.3l-288.5 0 5.4 28.5c2.2 11.3 12.1 19.5 23.6 19.5L488 336c13.3 0 24 10.7 24 24s-10.7 24-24 24l-288.3 0c-34.6 0-64.3-24.6-70.7-58.5L77.4 54.5c-.7-3.8-4-6.5-7.9-6.5L24 48C10.7 48 0 37.3 0 24zM128 464a48 48 0 1 1 96 0 48 48 0 1 1 -96 0zm336-48a48 48 0 1 1 0 96 48 48 0 1 1 0-96z"/>
    </svg>
    
    <div class="flex-container">
      <div
        v-for="item in items"
        :key="item.id"
        class="flex-item w-full max-w-sm bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700"
      >
        <a href="#">
          <img
            class="p-6 h-auto w-full"
            :src="item.image"
            :alt="item.title"
          />
        </a>
        <div class="px-5 pb-5">
          <a href="#">
            <h5 class="text-sm font-semibold tracking-tight text-gray-900 dark:text-white">
              {{ item.title }}
            </h5>
          </a>
          <div class="flex items-center mt-2.5 mb-5">
            <div class="flex items-center space-x-1 rtl:space-x-reverse">
              <svg
                v-for="star in 5"
                :key="star"
                class="w-5 h-5"
                :class="star <= Math.round(item.rating.rate) ? 'text-yellow-400' : 'text-gray-200 dark:text-gray-600'"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                viewBox="0 0 22 20"
              >
                <path d="M10.979 1.686c.437-1.098 1.91-1.098 2.347 0l2.056 5.166 5.384.78c1.201.174 1.681 1.65.81 2.497l-3.898 3.8.92 5.363c.211 1.232-1.083 2.165-2.202 1.586l-4.81-2.53-4.81 2.53c-1.119.579-2.413-.354-2.202-1.586l.92-5.363-3.898-3.8c-.872-.847-.391-2.323.81-2.497l5.384-.78L10.979 1.686z"/>
              </svg>
            </div>
            <span class="bg-blue-100 text-blue-800 text-xs font-semibold px-2.5 py-0.5 rounded dark:bg-blue-200 dark:text-blue-800 ms-3">
              {{ item.rating.rate }}
            </span>
          </div>
          <div class="flex items-center justify-between">
            <span class="text-2xl font-bold text-gray-900 dark:text-white">
              ${{ item.price }}
            </span>
            <a href="#" @click="toggleButton(item)"
              class="text-white bg-blue-700 hover:bg-blue-900 focus:ring-4 focus:outline-none focus:ring-blue-300 font-small rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
              {{ cartIncludes(item) ? 'Remove' : 'Add' }}
            </a>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Cart Display Section -->
    <div v-if="cart.length > 0" class="mt-10">
      <h2 class="text-xl font-bold mb-4">Cart Items</h2>
      <div v-for="cartItem in cart" :key="cartItem.id" class="flex items-center justify-between mb-4">
        <span class="text-lg font-semibold">{{ cartItem.title }}</span>
        <span class="text-lg font-semibold">${{ cartItem.price }}</span>
        <span class="text-lg font-semibold">x{{ cartItem.quantity }}</span>
      </div>
      <div class="flex items-center justify-between font-bold">
        <span>Total</span>
        <span>${{ cartTotal }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import CartData from './CartData.vue';
export default {

  components:{
     
    CartData

  },


  name: "HelloWorld",
  CartData,
  data() {
    return {
      items: [], // array to store the data fetched from API.
      cart: [],  // array to store items added to the cart
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        const data = await response.json();
        this.items = data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
    toggleButton(item) {
      const existingItem = this.cart.find(cartItem => cartItem.id === item.id);
      if (existingItem) {
        existingItem.quantity += 1;
        if (existingItem.quantity <= 0) {
          this.cart = this.cart.filter(cartItem => cartItem.id !== item.id);
        }
      } else {
        this.cart.push({ ...item, quantity: 1 });
      }
    },
    cartIncludes(item) {
      return this.cart.some(cartItem => cartItem.id === item.id);
    }
  },
  computed: {
    cartTotal() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0).toFixed(2);
    }
  }
};

    // getData() {
    //   this.content++;
    //   console.log('Content value:', this.content);
    // },
    
  
</script>

<style scoped>
.flex-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  gap: 20px;
  margin: 0 auto;
  max-width: 1200px;
  padding: 20px;
}

.flex-item {
  flex-basis: calc(25% - 20px);
  margin-bottom: 20px;
}

svg {
  width: 20px;
  height: 20px;
}
</style>
