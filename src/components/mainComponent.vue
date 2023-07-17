<script>
export default {
 
  props:{
    cardInfo: {
        type:Object,
        default:[]
    },
    image: {
        type:Array,
        default:[]
    }
  }
};

</script>

<template>
    <div class="fluid-container">
        <div class="col-auto">
            <select class="form-select" aria-label="Select a status">
                <option selected>alien</option>
                <option value="1">One</option>
                <option value="2">Two</option>
                <option value="3">Three</option>
            </select>

            <div class="my-container">
                <div class="quantity ">
                    <h4>found 39 cards</h4>
                </div>
                <div class="card-container"
                >
                    <div class="card"
                    v-for="(card, i) in cardInfo" :key="i">
                    <img :src="image[i]" alt="">
                        <h3> {{cardInfo[i].name }}</h3>
                        <h5>{{cardInfo[i].archetype}}</h5>
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
    height: 700px;
    background-color:#D48F38 ;
    text-align: center;
    flex-wrap: wrap;
    img{
        width: 100%;
        height: 500px;
    }
    h3{
        font-size: 2rem;
        color: white;
        font-weight: bold;
    }
    h5{
        font-size: 1.2rem;
        font-weight: lighter;
    }
}
   

</style>