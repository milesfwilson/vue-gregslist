<template>
  <div class="houses-page container-fluid text-center">
    <button class="btn bg-transparent m-3"
            type="button"
            data-toggle="collapse"
            data-target="#houseForm"
            aria-expanded="false"
            aria-controls="contentId"
    >
      <div class="d-flex">
        <i class="fa fa-plus-circle fa-2x my-auto" aria-hidden="true"></i>
        <h1 class=" my-auto pl-2">
          House
        </h1>
      </div>
    </button>

    <div class="col-8 offset-2 collapse" id="houseForm">
      <form class="form-group" @submit.prevent="createHouse">
        <div class="row">
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Bedrooms"
                   v-model="state.newHouse.bedrooms"
            >
          </div>
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Bathrooms"
                   v-model="state.newHouse.bathrooms"
            >
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Levels"
                   v-model="state.newHouse.levels"
            >
          </div>
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Year"
                   v-model="state.newHouse.year"
            >
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Price"
                   v-model="state.newHouse.price"
            >
          </div>
          <div class="col-6">
            <input type="text"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Image URL"
                   v-model="state.newHouse.imgUrl"
            >
          </div>
        </div>
        <input type="text"
               class="form-control my-1"
               aria-describedby="helpId"
               placeholder="Description"
               v-model="state.newHouse.description"
        >

        <button type="submit" class="btn btn-primary m-3">
          Create
        </button>
      </form>
    </div>

    <div class="row">
      <house-component v-for="house in houses" :key="house._id" :house-prop="house" />
    </div>
  </div>
</template>

<script>
import { onMounted, computed, reactive } from 'vue'
import { housesService } from '../services/HousesService'
import HouseComponent from '../components/HouseComponent'
import { AppState } from '../AppState'

export default {
  name: 'HousesPage',
  components: { HouseComponent },
  setup() {
    const state = reactive({
      newHouse: {

      }
    })
    onMounted(() => {
      housesService.getAllHouses()
    })
    return {
      state,
      houses: computed(() => AppState.houses),
      createHouse() {
        housesService.createHouse(state.newHouse)
      }
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
