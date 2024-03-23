<template>
  <BannerCard />
  <RegistrationForm />
</template>

<script>
import BannerCard from './components/BannerCard.vue'
import RegistrationForm from './components/RegistrationForm.vue'

export default {
  name: 'App',
  components: {
    BannerCard,
    RegistrationForm
  }
}
</script>

<style>

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}

.body {
    display: flex;
    height: 100vh;
    justify-content: center;
    align-items: center;
}
</style>
