<script>
import headerComponent from './components/headerComponent.vue';
import mainComponent from './components/mainComponent.vue';
import axios from 'axios' ;

export default {
  name: "app",
  components: {
    headerComponent,
    mainComponent,
  
  },
  data() {
    return{
      loading: true,
      cardInfo: [],
      image: []
    };
  },
  created() {
    axios
      .get("https://db.ygoprodeck.com/api/v7/cardinfo.php")
      .then(response =>  {
        console.log(response.data.data);
        
        this.cardInfo = response.data.data
        
        this.image = this.cardInfo.map(obj => obj.card_images[0].image_url)
        console.log(this.image[1]);
        this.loading = false;
      });
  }
};
</script>

<template>
  <headerComponent/>
  <div v-if="loading">
      <div class="caricamento"> <p>Caricamento in corso...</p></div>
      
    </div>
    <div  v-else>
  <mainComponent :cardInfo="cardInfo" :image="image"/></div>


</template>

<style lang="scss" scoped>
@use "assets/scss/main";
body{
  margin: 0;
}

#app{
  margin: 0;
  padding: 0;
}
.caricamento{
  width: 80%;
  margin: 0 auto;
  display: flex; 
  align-items: center;
  height: 900px;
  background-image: url(./assets/img/3e024-ragazzamaganera4_full.png);
  background-repeat: no-repeat;
  p{
    font-size: 10rem;
    color: purple;
    text-align: center;
    
  }
}
</style>
