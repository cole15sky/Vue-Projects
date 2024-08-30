<template>
<div>
  <h2>Shopping Cart</h2>

<table >
  <tr>
    <th>id</th>
    <th>price</th>
    <th>category</th>
  </tr>
  <tr>
    <td> z</td>
    <td> y</td>
    <td>x</td>
  </tr>
  <tr>
    <td> a</td>
    <td> c</td>
    <td>b</td>
  </tr>
</table>


</div>
</template>




 <script>
fetch('https://fakestoreapi.com/products')
.then(res =>{
return res.json();
})

.then(data =>{
data.forEach(user =>{
  const markup = `<th>$(user.id)</th>`;
   console.log(user.description);
   document.querySelector('tr').insertAdjacentHTML('beforeend',markup)
});

})

.catch(error => console.log(error));

</script>



<style scoped>
table, th, td {
  border:1px solid black;
}
table{
  width: 100%;
}
</style>

