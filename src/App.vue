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
      cardInfo: [],
      image: []
    };
  },
  created() {
    axios
      .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0")
      .then(response =>  {
        console.log(response.data.data);
        
        this.cardInfo = response.data.data
        
        this.image = this.cardInfo.map(obj => obj.card_images[0].image_url)
        console.log(this.image[1]);
      });
  }
};
</script>

<template>
  <headerComponent/>

  <mainComponent :cardInfo="cardInfo" :image="image"/>


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
</style>
