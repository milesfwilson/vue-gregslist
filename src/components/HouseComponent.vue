<template>
  <div class="house-component col-4 mt-2">
    <div class="card shadow-lg m-2 p-2 text-center">
      <router-link :to="{name: 'ActiveHouse' , params: {houseId: houseProp._id}}">
        <img :src="houseProp.imgUrl" class="img-fluid" alt="">
      </router-link>

      <h5 class="mt-2">
        {{ houseProp.bedrooms }} Bed {{ houseProp.bathrooms }} Bath
      </h5>
      <h5>
        {{ houseProp.levels }} Floor
      </h5>
      <h4>
        {{ houseProp.year }}
      </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HouseComponent',
  props: ['houseProp'],
  setup() {
    return {}
  },
  components: {}
}
</script>

<style lang="scss" scoped>

</style>
