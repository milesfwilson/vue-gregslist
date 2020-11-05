<template>
  <div class="cars-page container-fluid text-center">
    <button class="btn bg-transparent"
            type="button"
            data-toggle="collapse"
            data-target="#carForm"
            aria-expanded="false"
            aria-controls="contentId"
    >
      <h1>Add Car</h1>
    </button>

    <div class="col-8 offset-2 collapse" id="carForm">
      <form class="form-group" @submit.prevent="createCar">
        <div class="row">
          <div class="col-6">
            <input type="text"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Make"
                   v-model="state.newCar.make"
            >
          </div>
          <div class="col-6">
            <input type="text"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Model"
                   v-model="state.newCar.model"
            >
          </div>
        </div>
        <div class="row">
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Year"
                   v-model="state.newCar.year"
            >
          </div>
          <div class="col-6">
            <input type="number"
                   class="form-control my-1"
                   aria-describedby="helpId"
                   placeholder="Price"
                   v-model="state.newCar.price"
            >
          </div>
        </div>
        <input type="text"
               class="form-control my-1"
               aria-describedby="helpId"
               placeholder="Description"
               v-model="state.newCar.description"
        >
        <input type="text"
               class="form-control my-1"
               aria-describedby="helpId"
               placeholder="Image URL"
               v-model="state.newCar.imgUrl"
        >

        <button type="submit" class="btn btn-primary">
          Create
        </button>
      </form>
    </div>
    <div class="row">
      <car-component v-for="car in cars" :key="car._id" :car-prop="car" />
    </div>
  </div>
</template>

<script>
import { computed, onMounted, reactive } from 'vue'
import { carsService } from '../services/CarsService'
import CarComponent from '../components/CarComponent'
import { AppState } from '../AppState'
export default {
  name: 'CarsPage',
  components: { CarComponent },
  setup() {
    const state = reactive({
      newCar: {}
    })
    onMounted(() => {
      carsService.getAllCars()
    })
    return {
      state,
      cars: computed(() => AppState.cars),
      createCar() {
        carsService.createCar(state.newCar)
      }
    }
  }
}
</script>

<style scoped>

</style>
