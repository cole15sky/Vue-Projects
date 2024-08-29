<template>
  <div class="wrapper">
    <div class="container">
      <h3>ShoppingCart.</h3> 
      <div class="items">
        <ol>
        <li>Merlot Red
          <button> + </button>
          <button> - </button> 
          <sub> $ 450</sub>          

        </li>
        <li>Airen White

          <button> + </button>
          <button> - </button>
          <sub> $ 350</sub>          

        </li>
        
        <li>Antinori
          
          <button> + </button>
          <button> - </button>
          <sub> $ 650</sub>          
        </li>
          
      </ol>
      </div>
      
      

     <h4> Thanks! Visit Again</h4>


    </div>
</div>
</template>

<script>
export default {
  name: "ShoppingCart",
};
</script>

<style scoped>
h3{
  margin-left:35%;
}

.wrapper {
  display: flex;
  justify-content: center; 
  align-items: center; 
  height: 120vh;
  background-color: aquamarine;
}
.container{
  width: 500px;
  height: 500px;
  border: 1px solid blue;
  background-color: turquoise;
}

.items{
  background-color:cadetblue;
  height: 390px;
  width: 500px;
}

h4{
  margin-left: 35%;
  color: darkgreen;
}


li{
  font-size: 20px;
padding: 20px;
} 

sub{
  margin-left: 190px;
}




</style>
