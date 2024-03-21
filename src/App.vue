<template>
  <BannerCard />
</template>

<script>
import BannerCard from './components/BannerCard.vue'

export default {
  name: 'App',
  components: {
    BannerCard
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
