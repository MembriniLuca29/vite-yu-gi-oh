<script>
import headerComponent from './components/headerComponent.vue';
import mainComponent from './components/mainComponent.vue';
import axios from 'axios' ;
import { store } from './store.js';

export default {
  name: "app",
  components: {
    headerComponent,
    mainComponent,
  
  },
  data() {
    return {
      
            store:store,
        };
  },
  created() {
    axios
      .get("https://db.ygoprodeck.com/api/v7/cardinfo.php")
      .then(response =>  {
        console.log(response.data.data);
        
        this.store.cardInfo = response.data.data;
        this.store.image = this.store.cardInfo.map(obj => obj.card_images[0].image_url);
        console.log(this.store.image[1]);
        this.store.loading = false;
      });
  }
};
</script>

<template>
  <headerComponent/>
  <div v-if="store.loading">
      <div class="caricamento"> <p>Caricamento in corso...</p></div>
      
    </div>
    <div  v-else>
  <mainComponent :cardInfo="store.cardInfo" :image="store.image"/></div>


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
  background-image: url(./assets/img/la-giovane-maga-nera-yu-gi-oh-raddoppia-quest-ultimo-cosplay-v3-432482-1280x960.jpg);
  background-repeat: no-repeat;
  transition: 2s ease-in-out;
  p{
    font-size: 10rem;
    color: blue;
    text-align: center;
    font-weight: bold;
  }
}
</style>
