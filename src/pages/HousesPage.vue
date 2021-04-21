<template>
  <div class="houses container">
    <div class="row">
      <div class="col  py-3">
        <h2>Houses</h2>
        <button title="Open Create House Form"
                type="button"
                class="btn btn-outline-success"
                data-toggle="modal"
                data-target="#house"
        >
          <i class="fas fa-plus" aria-hidden="true"></i>
        </button>
      </div>
    </div>
    <div class="row">
      <House v-for="house in state.houses" :key="house.id" :house="house" />
    </div>
    <modal />
  </div>
</template>

<script>
import { reactive, computed, onMounted } from 'vue'
import { AppState } from '../AppState'
import House from '../components/HouseComponent'
import { housesService } from '../services/HousesService'
import modal from '../components/CreateHouseModal'

export default {
  name: 'Houses',
  setup() {
    const state = reactive({
      houses: computed(() => AppState.houses)
    })
    onMounted(async() => {
      try {
        await housesService.getHouses()
      } catch (error) {
        console.error(error)
      }
    })

    return {
      state
    }
  },
  components: {
    House,
    modal
  }
}
</script>

<style lang="scss" scoped>

</style>
