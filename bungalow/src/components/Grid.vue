<template>
    <div class="flex-grid">
        <div
          class="card"
          style="width: 18rem;"
          v-for="property in properties"
          v-bind:key=property.id
        >
          <Card
            v-bind:property="property"
            v-bind:image="imageIndexMap && property.images[imageIndexMap[property.id]] || property.images[0]"
            :callback="(clickedPropertyId, direction) => updateImageIndex(clickedPropertyId, direction, property.images.length)"
          />
        </div>
    </div>
</template>

<script>
    import Card from "./Card"
    import axios from "axios";


    export default {
        name: 'Grid',
        components: {
          Card
        },
        data() {
            return {
                properties: [
                    {
                        images: []
                    }
                ],
                // maps propery id of card to index of image we want to display
                imageIndexMap: null,
            };
        },
        methods: {
            updateImageIndex: function(clickedPropertyId, direction, maxImagesCount) {
                if (this.imageIndexMap && (this.imageIndexMap[clickedPropertyId] || this.imageIndexMap[clickedPropertyId] === 0)) {
                  if (direction === "previous" && this.imageIndexMap[clickedPropertyId] !== 0) {
                    this.imageIndexMap[clickedPropertyId] -= 1
                  } else {
                    // we do not want to set an index that is out of bounds
                    if (this.imageIndexMap[clickedPropertyId] + 1 < maxImagesCount - 1) {
                      this.imageIndexMap[clickedPropertyId] += 1
                    }
                  }
                } else {
                  this.imageIndexMap = {
                    ...this.imageIndexMap,
                    [clickedPropertyId]: 1
                  }
                }
            }
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
    height: 500px;
    margin-bottom: 12px;
  }

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