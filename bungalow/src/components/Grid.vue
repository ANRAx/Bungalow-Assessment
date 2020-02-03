<template>
    <div class="flex-grid">
        <div class="card" style="width: 18rem;" v-for="property in properties" v-bind:key=property.id>
            <img
             class="card-image"
             v-bind:src="property.images && property.images[0] && property.images[0].md_url || 'https://cdn.pixabay.com/photo/2017/07/28/23/18/coming-soon-2550190_960_720.jpg'">
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
    name: 'Grid',
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
</style>