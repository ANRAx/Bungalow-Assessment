<template>
    <div class="flex-grid">
        <div class="card" style="width: 18rem;" v-for="property in properties" v-bind:key=property.id>
            <img v-bind:src="property.images && property.images[0] && property.images[0].md_url" class="card-image">
            <div class="card-body">
                <p class="card-text">{{property.headline}}</p>
                <p class="card-text">{{property.available_room_count}} of {{property.total_room_count}} rooms available</p>
                <p class="card-text">${{property.room_prices[0]}}</p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Card',
    data() {
        return {
            properties: [
                {
                    images: []
                }
            ]
        };
    },    

    created: function() {
        axios
            .get('https://stage-fieldstone.bungalow.com/api/v1/listings/properties/?market__slug=seattle')
            .then(res => {
                this.properties = res.data.results;
            })
    }
}
</script>

<style scoped>
.flex-grid {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    margin: 50px 25px 0 25px;
  }

  .card {
    flex: 0 1 24%;
    margin-bottom: 15px;
  }

 .card > img {
     height: 315px;
 }

    @media screen and (max-width: 480px) {
        .card {
            flex: 0 1 99%
        }
    }

    @media only screen and (min-width: 481px) and (max-width: 900px) {
        .card {
            flex: 0 1 32%
        }

        .card > img {
            height: 180px;
        }
    }

    @media only screen and (min-width: 901px) and (max-width: 1024px) {
        .card {
            flex: 0 1 24%
        }
    }



  
</style>