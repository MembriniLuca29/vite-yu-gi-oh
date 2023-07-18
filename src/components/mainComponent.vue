<script>
import { store } from '../store.js';
import axios from 'axios';

export default {
  data() {
    return {
      store: store,
      archetypes: [],
      selectedArchetype: "", // Archetipo selezionato nella select
    };
  },
  props: {
    cardInfo: {
      type: Object,
      default: [],
    },
    image: {
      type: Array,
      default: [],
    },
  },
  created() {
    this.fetchArchetypes();
  },
  methods: {
    fetchArchetypes() {
      axios
        .get("https://db.ygoprodeck.com/api/v7/archetypes.php")
        .then(response => {
          this.archetypes = response.data;
          console.log(this.archetypes[0].archetype_name);
        })
        .catch(error => {
          console.log('Errore nella chiamata');
        });
    },
    filterByArchetype() {
      if (this.selectedArchetype == "") {
        return this.cardInfo;
      } else {
        return this.cardInfo.filter(
          card => card.archetype == this.selectedArchetype
        );
      }
    },
  },
  computed: {
    filteredCardInfo() {
      return this.filterByArchetype();
    },
    filteredImages() {
      const filteredCardInfo = this.filterByArchetype();
      return filteredCardInfo.map(obj => obj.card_images[0].image_url);
    },
  },
};
</script>

<template>
  <div class="fluid-container">
    <div class="col-auto">
      <form action="">
        <select class="form-select" aria-label="Select an archetype" v-model="selectedArchetype">
          <option value="">All Archetypes</option>
          <option v-for="archetype in archetypes" :value="archetype.archetype_name" :key="archetype.archetype_name">
            {{ archetype.archetype_name }}
          </option>
        </select>
      </form>

      <div class="my-container">
        <div class="quantity">
          <h4>found {{ filteredCardInfo.length }} cards</h4>
        </div>
        <div class="card-container">
          <div class="card" v-for="(card, i) in filteredCardInfo" :key="i">
            <img :src="filteredImages[i]" alt="">
            <h3>{{ card.name }}</h3>
            <h5>{{ card.archetype }}</h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>




<style lang="scss" scoped>
    .fluid-container{
        background-color: #D48F38;
        select{
            margin: 40px 200px;
            padding: 10px 80px 10px 0px;
            font-size: 1.5rem;
        }
        .my-container{
            width: 80%;
            margin: 0 auto;
            padding: 30px 30px;
            background-color: white;
            .quantity{
                background-color:#212529 ;
                color: white;
                padding: 1px 20px;
                font-size: 1.4rem;
                margin: 0 10px;
            }
            .card-container{
                width: 100%;
                display: flex;
                justify-content: space-between;
                flex-wrap: wrap;
            }
        }
    }
    .card{
    margin: 0 10px 10px 10px;
    width: calc((100% / 5) - 20px );
    min-height: 400px;
    background-color:#D48F38 ;
    text-align: center;
    flex-wrap: wrap;
    img{
        width: 100%;
        max-height: 70%;
    }
    h3{
        font-size: 2rem;
        color: white;
        font-weight: bold;
        height:10%;
    }
    h5{
        font-size: 1.2rem;
        font-weight: lighter;
        height: 15%;
    }
}
   
</style>