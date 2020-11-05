<template>
  <div class="active-house container-fluid">
    <div class="row mt-5">
      <div class="col-4 offset-2 bg-dark">
        <div class="p-3">
          <img :src="house.imgUrl" class="img-fluid img-thumbnail rounded" alt="">
        </div>
      </div>
      <div class="col-4 bg-dark text-light">
        <div class="py-3">
          <div class="d-flex">
            <h4 class="mt-2">
              {{ house.bedrooms }} Bedrooms
            </h4>
            <div class="ml-auto">
              <button class="btn bg-transparent text-light" @click="goBack">
                <i class="fas fa-long-arrow-alt-left"></i>
              </button>
              <button class="btn bg-transparent text-light" @click="removeHouse">
                <i class="fa fa-trash text-light" aria-hidden="true"></i>
              </button>
            </div>
          </div>
          <h4>
            {{ house.bathrooms }} Bathrooms
          </h4>
          <h4>
            {{ house.levels }} Floor
          </h4>
          <h4>
            Built in {{ house.year }}
          </h4>
          <h4>
            ${{ house.price }}
          </h4>
        </div>
      </div>
    </div>
    <div class="row">
      <div class="col-8 offset-2 bg-dark text-light text-center">
        <h4 class="p-3">
          {{ house.description }}
        </h4>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, onMounted } from 'vue'
import { housesService } from '../services/HousesService'
import { AppState } from '../AppState'
import { useRoute } from 'vue-router'
export default {
  name: 'ActiveHouse',
  setup() {
    const route = useRoute()
    onMounted(() => {
      housesService.getActiveHouse(route.params.houseId)
    })
    return {
      house: computed(() => AppState.activeHouse),
      removeHouse() {
        housesService.removeHouse(route.params.houseId)
      },
      goBack() {
        housesService.goBack()
      }
    }
  },
  components: {

  }
}
</script>

<style lang="scss" scoped>

</style>
