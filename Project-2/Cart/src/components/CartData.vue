<template>
    <div>
        <h1>This Page stores the {{cart}} history.</h1>
    </div>
    
</template>


<script> 
export default{
    name:'CartData',

    data(){
        return{
            item: cart 
        }
    }
}

</script>

<style scoped>

</style>