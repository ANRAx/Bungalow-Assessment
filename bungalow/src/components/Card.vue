<template>
  <div>
    <div id="carouselExampleControls" class="carousel slide" data-ride="carousel">
        <div class="carousel-inner">
          <div class="carousel-item active">
              <img
                  class="d-block w-100 card-image"
                  v-bind:src="image && image.md_url || 'https://cdn.pixabay.com/photo/2017/07/28/23/18/coming-soon-2550190_1280.jpg' "
              >
          </div>
        </div>
        <a
          class="carousel-control-prev"
          href="#carouselExampleControls"
          role="button" data-slide="prev"
          v-if="image"
          v-on:click="callback(property.id, 'previous')"
        >
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="sr-only">Previous</span>
        </a>
        <a
          class="carousel-control-next"
          href="#carouselExampleControls"
          role="button"
          data-slide="next"
          v-if="image"
          v-on:click="callback(property.id, 'next')"
        >
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="sr-only">Next</span>
        </a>
    </div>
    <div class="card-body">
        <p class="card-text">{{property.headline}}</p>
        <p class="card-text">{{property.available_room_count}} of {{property.total_room_count}} rooms available</p>
        <p class="card-text">${{property.room_prices[0]}}</p>
    </div>
  </div>
</template>

<script>
    export default {
        name: 'Card',
        props: {
          property: {
            type: Object
          },
          callback: {
            type: Function
          },
          image: {
            type: Object
          },
        },
    }
</script>

<style scoped>
  .card-image {
    height: 315px;
  }

  @media screen and (max-width: 480px) {
    .card {
      flex: 0 1 99%;
    }
  }

  @media only screen and (min-width: 481px) and (max-width: 700px) {
    .card {
      flex: 0 1 32%;
    }

    .card > img {
      height: 180px;
    }
  }

  @media only screen and (min-width: 701px) and (max-width: 1024px) {
    .card {
      flex: 0 1 24%;
    }

    .card > img {
      height: 180px;
    }
  }

</style>