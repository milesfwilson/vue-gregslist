<template>
  <div id="nav" class="bg-dark text-light py-3 d-flex">
    <h3 class="mx-2">
      GregsList
    </h3>
    <router-link class="text-light m-2" to="/">
      Home
    </router-link>
    <router-link class="text-light m-2" to="/about">
      About
    </router-link>
    <!-- able to router-link with just /pathName but using a named route is much safer -->
    <!-- <router-link to="/cars">
      Cars
    </router-link> -->
    <router-link class="text-light m-2" :to="{name: 'Cars'}">
      Cars
    </router-link>
    <router-link class="text-light m-2" :to="{name: 'Houses'}">
      Houses
    </router-link>
  </div>
  <router-view />
</template>

<script>
import { computed } from 'vue'
import { AppState } from './AppState'
export default {
  setup() {
    return { appState: computed(() => AppState) }
  }
}
</script>
