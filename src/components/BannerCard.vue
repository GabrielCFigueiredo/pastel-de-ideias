<template>
    <form action="" @submit.prevent="submitForm">
    <input type="text" v-model="nome">
    <button>Enviar</button>
  </form>
</template>

<script>
export default {
  name: 'BannerCard',
  data () {
    return {
      nome: ''
    }
  },
  methods: {
    submitForm () {
      console.log(this.nome)
    }
  }
}
</script>
