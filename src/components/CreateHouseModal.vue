<template>
  <div class="modal fade"
       id="house"
       tabindex="-1"
       role="dialog"
       aria-labelledby="ModalLabel"
       aria-hidden="true"
  >
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="ModalLabel">
            New House
          </h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <form @submit.prevent="createHouse">
          <div class="modal-body">
            <div class="form-group">
              <label for="bathrooms">Bathrooms</label>
              <input type="number"
                     class="form-control"
                     id="bathrooms"
                     placeholder="Bathrooms..."
                     v-model="state.newHouse.bathrooms"
                     required
              >
            </div>
            <div class="form-group">
              <label for="bedrooms">Bedrooms</label>
              <input type="number"
                     class="form-control"
                     id="bedrooms"
                     placeholder="Bedrooms..."
                     v-model="state.newHouse.bedrooms"
                     required
              >
            </div>
            <div class="form-group">
              <label for="levels">Levels</label>
              <input type="number"
                     class="form-control"
                     id="levels"
                     placeholder="Levels..."
                     v-model="state.newHouse.levels"
                     required
              >
            </div>
            <div class="form-group">
              <label for="year">Year</label>
              <input type="number"
                     class="form-control"
                     id="year"
                     placeholder="Year..."
                     v-model="state.newHouse.year"
                     required
              >
            </div>
            <div class="form-group">
              <label for="price">Price</label>
              <input type="number"
                     class="form-control"
                     id="price"
                     placeholder="Price..."
                     min="1"
                     v-model="state.newHouse.price"
              >
            </div>
            <div class="form-group">
              <label for="description">Description</label>
              <input type="text"
                     class="form-control"
                     id="description"
                     placeholder="Description..."
                     minlength="3"
                     maxlength="20"
                     v-model="state.newHouse.description"
              >
            </div>
            <div class="form-group">
              <label for="imgUrl">Image Url</label>
              <input type="text" class="form-control" id="imgUrl" placeholder="Url..." v-model="state.newHouse.imgUrl">
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">
              Close
            </button>
            <button type="submit" class="btn btn-primary">
              Create
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'
import { housesService } from '../services/HousesService'
import $ from 'jquery'
export default {
  name: 'Component',
  setup() {
    const state = reactive({
      newHouse: {}
    })
    return {
      state,
      async createHouse() {
        try {
          await housesService.createHouse(state.newHouse)
          state.newHouse = {}
          $('#house').modal('hide')
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
