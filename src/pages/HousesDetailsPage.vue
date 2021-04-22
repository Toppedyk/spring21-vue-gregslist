<template>
  <div v-if="state.loading == true">
    <h1>Loading Data</h1>
  </div>
  <div class="house-details" v-else>
    <h1>House Details!</h1>
    <div class="card shadow">
      <img class="card-img-top" :src="state.house.imgUrl" alt="">
      <div class="card-body">
        <h3>
          Listing Price: ${{ state.house.price }}
        </h3>
        <h5 class="card-title">
          Bedrooms: {{ state.house.bedrooms }} | Bathrooms: {{ state.house.bathrooms }}
        </h5>
      </div>
      <button type="button" class="btn btn-danger" @click="deleteHouse(state.house.id)">
        Delete Listing
      </button>
    </div>
  </div>
</template>

<script>
import { reactive, computed, onMounted } from 'vue'
import { AppState } from '../AppState'
import { housesService } from '../services/HousesService'
import { useRoute, useRouter } from 'vue-router'
export default {
  name: 'HouseDetails',
  setup() {
    const route = useRoute()
    const router = useRouter()
    // ROUTER is the toolset of changing routes automatically
    const state = reactive({
      loading: true,
      house: computed(() => AppState.activeHouse)
    })

    onMounted(async() => {
      try {
        await housesService.getHouseById(route.params.id)
        state.loading = false
      } catch (error) {
        console.error(error)
      }
    })

    return {
      state,
      async deleteHouse(id) {
        try {
          await housesService.deleteHouse(id)
          AppState.activeCar = null
          router.push({ name: 'Houses' })
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
