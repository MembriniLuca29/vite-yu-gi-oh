<script>
import { store } from '../store.js';

export default {
    name: "HeaderComponent",
    data() {
        return {
            store
        }
    },
    methods: {

    }
}
</script>

<template>
    
       
    <div class="d-flex align-items-center ">
         <img src="../assets/img/1200px-Yu-Gi-Oh!_(Logo).jpg" alt="" class="rounded float-start ">  
         <h2 class="fs-1">Yu-Gi-Oh Api</h2>
    </div>  
      
</template>

<style lang="scss" scoped>
img{
    max-height: 50px;
}
h2{
    font-size: 30px;
}
</style>