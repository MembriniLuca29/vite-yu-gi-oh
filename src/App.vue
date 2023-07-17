<script>
import headerComponent from './components/headerComponent.vue';
import mainComponent from './components/mainComponent.vue';

export default {
  name: "app",
  components: {
    headerComponent,
    mainComponent,
  
  },
};
</script>

<template>
  <headerComponent/>

  <mainComponent/>


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
