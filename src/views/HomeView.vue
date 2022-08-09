<template>
  <BannerComponent/>
  <BurgerForms/>
</template>

<script lang="ts">

import BannerComponent from "../components/Banner.vue"
import BurgerForms from "../components/BurgerForms.vue"

export default{
  name: "HomeView",
  components: {
    BannerComponent,
    BurgerForms
  }
}
</script>

<style scoped>

</style>