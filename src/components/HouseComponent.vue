<template>
  <div class="house col-md-4 mb-3">
    <router-link :to="{name: 'HouseDetails', params: { id: house.id }}">
      <div class="card shadow">
        <img class="card-img-top" :src="house.imgUrl" alt="">
        <div class="card-body">
          <h3>
            Listing Price: ${{ house.price }}
          </h3>
          <h5 class="card-title">
            Bedrooms: {{ house.bedrooms }} | Bathrooms: {{ house.bathrooms }}
          </h5>
        </div>
      </div>
    </router-link>
    <div>
      <button type="button" class="btn btn-danger" @click="deleteHouse(house.id)">
        Delete Listing
      </button>
    </div>
  </div>
</template>

<script>
import { housesService } from '../services/HousesService'
export default {
  name: 'House',
  props: {
    house: {
      type: Object,
      required: true
    }
  },
  setup() {
    return {
      async deleteHouse(id) {
        try {
          await housesService.deleteHouse(id)
        } catch (error) {
          console.error(error)
        }
      }
    }
  },
  components: {}
}
</script>

<style lang="scss" scoped>

</style>
