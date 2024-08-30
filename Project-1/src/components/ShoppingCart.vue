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
        </tr>
      </thead>
      <tbody>
        <!-- Use v-for to loop through the fetched data -->
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.id }}</td>
          <td>{{ product.price }}</td>
          <td>{{ product.category }}</td>
          <td>{{ product.title }}</td>
        </tr>
      </tbody>
    </table>


</div>
</template>




 <script>
// fetch('https://fakestoreapi.com/products')
// .then(res =>{
// return res.json();
// })

// .then(data =>{
// data.forEach(user =>{
//   const markup = `<th>$(user.id)</th>`;
//    console.log(user.description);
//    document.querySelector('td').insertAdjacentHTML('beforeend',markup)
// });

// })

// .catch(error => console.log(error));


import { ref, onMounted } from 'vue';

export default {
  setup() {
    const products = ref([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        products.value = await response.json();
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    onMounted(() => {
      fetchProducts();
    });

    return {
      products
    };
  }
};

</script>



<style scoped>
table, th, td {
  border:1px solid black;
}
table{
  width: 100%;
}
</style>

