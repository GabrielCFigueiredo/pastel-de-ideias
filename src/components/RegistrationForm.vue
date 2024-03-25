<template>
<div class="container">
    <div class="card-form">
        <header class="card-title">
            <h3>Monte aqui seu cardápio. O que está esperando?</h3>
        </header>
        <form class="form-card-group" @submit.prevent="submitForm">
            <section class="card">
                <div class="card-input">
                    <input
                    id="title-product"
                    class="title-product"
                    type="text"
                    placeholder="Título do Pedido"
                    v-model="name"
                    required
                    minlength="3"
                    maxlength="60" />
                </div>
                <div class="card-input">
                    <input
                    id="flavor-product"
                    class="flavor-product"
                    type="text"
                    placeholder="Sabor"
                    v-model="flavor"
                    required
                    minlength="3"
                    maxlength="60" />
                </div>
                <div class="card-input">
                    <input
                    id="price-product"
                    class="price-product"
                    type="number"
                    placeholder="R$"
                    v-model="price"
                    required />
                </div>
                <div class="card-description">
                    <textarea id="description"
                    class="description"
                    placeholder="Descrição"
                    v-model="description"
                    required>
                </textarea>
                </div>
                <div class="card-preview">
                <div
                    class="image-preview"
                    :style="{'background-image': `url(${previewImage})`}"
                    @click="selectImage">
                </div>
                    <input
                    id="image-upload"
                    ref="fileInput"
                    type="file"
                    @input='pickFile'>
                </div>
                <div class="card-pastries">
                    <img
                    class="pastries"
                    src="../../public/pastel-desfocado.png"
                    alt="">
                </div>
                <div class="card-btn">
                    <button
                    class="btn-cancel"
                    @click="cancelForm"
                    type="button">Cancelar</button>
                    <button
                    class="btn-register"
                    type="submit">Cadastrar</button>
                </div>
            </section>
        </form>
    </div>
    <section class="card-order" v-for="product in reversedResult" :key="product">
        <div class="order">
            <h2 class="product-request-title">{{ product.name }}</h2>
            <h2 class="asking-price">R$ {{ product.price }},00</h2>
        </div>
        <img class="image" :src='product.image' alt="suco">
        <div>
            <h3>Sabor: {{ product.flavor }}</h3>
            <h3>Descrição: {{ product.description }}</h3>
        </div>
    </section>
</div>
</template>
<script>
export default {
  name: 'RegistrationForm',
  data () {
    return {
      result: [],
      name: '',
      flavor: '',
      price: '',
      description: '',
      previewImage: null
    }
  },
  computed: {
    reversedResult () {
      return this.result.slice().reverse()
    }
  },

  methods: {
    async submitForm () {
      const data = {
        name: this.name,
        flavor: this.flavor,
        price: this.price,
        description: this.description
      }
      this.result.push(data)
      console.log(data)
      this.clear()
      this.name = ''
      this.flavor = ''
      this.price = ''
      this.description = ''
    },
    selectImage () {
      this.$refs.fileInput.click()
    },
    pickFile () {
      const input = this.$refs.fileInput
      const file = input.files
      const typeImage = ['image/png', 'image/jpeg']
      if (file && file[0]) {
        const fileTypes = file[0].type
        if (typeImage.includes(fileTypes)) {
          const reader = new FileReader()
          reader.onload = e => {
            this.previewImage = e.target.result
          }
          reader.readAsDataURL(file[0])
          this.$emit('input', file[0])
        } else {
          alert('Por favor, selecione um arquivo PNG ou JPG.')
        }
      }
    },
    cancelForm () {
      this.clear()
    },
    clear () {
      this.name = ''
      this.flavor = ''
      this.price = ''
      this.description = ''
      this.image = ''
      this.previewImage = null
    }
  }
}
</script>
<style>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
.card-form {
    width: 100%;
    max-width: 1200px;
    border-radius: 10px;
    box-shadow: 0 0 15px black;
    display: flex;
    flex-direction: column;
    gap: 12px;
    border: 1px solid black;
    position: absolute;
    top: 325px;
    background: #FFF;
}

.card {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
}

h3 {
    color: #AD4925;
    font-weight: 600;
}

.card-title {
    background-color: #F9CB32;
    border-radius: 10px 10px 0 0;
    height: 40px;
    display: flex;
    align-items: center;
    padding: 10px;
}

.card-input:nth-child(2n) {
    justify-content: end;
}

.card-input {
display: flex;
flex-wrap: wrap;
justify-content: end;
flex-grow: 1;
padding: 0 12px;
padding-bottom: 15px;
}

.title-product {
    width: 100%;
    padding: 10px;
    outline: none;
    border-radius: 7px;
    border: 1px solid #A43C23;
}

.title-product::placeholder {
    color: #A43C23;
}

.price-product {
    width: 50%;
    padding: 10px;
    outline: none;
    border-radius: 7px;
    border: 1px solid #A43C23;
}

.price-product::placeholder {
    color: #A43C23;
}

.flavor-product {
    width: 100%;
    padding: 10px;
    outline: none;
    border-radius: 7px;
    border: 1px solid #A43C23;
}

.flavor-product::placeholder {
    color: #A43C23;
}

.card-description {
    width: 100%;
    height: 20%;
    padding: 0 0 0 12px;
}

.description {
    width: 99%;
    padding: 10px;
    outline: none;
    border-radius: 7px;
    border: 1px solid #A43C23;
}

.description::placeholder {
    color: #A43C23;
}

.image-preview {
    width: 100%;
    height: 100%;
    padding: 10px;
    outline: none;
    border-radius: 7px;
    border: 1px solid #A43C23;
    display: block;
    cursor: pointer;
    background-size: cover;
    background-position: center center;
    border: 1px solid #A43C23;
}

.card-pastries {
    width: 100%;
    height: 10vh;
}
.pastries {
    position: absolute;
    width: 70%;
    height: 395px;
    bottom: 328px;
    right:820px;
    transform: rotateY(55deg);
    filter: blur(4px);
}

.order {
    display: flex;
    justify-content: space-between;
    background-color: #E53F36;
    padding: 20px 0;
}

.order h2 {
    padding: 0 20px;
}

div h3 {
    padding: 10px 20px;
}

.asking-price {
    color: #FFF;
}

.form-card-group {
}

.card-preview {
    width: 100%;
    padding: 10px;
    height: 200px;
}

.card-btn {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    position: absolute;
    top: 449px;
}
.btn-cancel {
  box-sizing: border-box;
  appearance: none;
  background-color: #F9CB32;
  border: 2px solid #F9CB32;
  border-radius: 20px;
  color: #A43C23;
  cursor: pointer;
  display: flex;
  align-self: center;
  font-size: 16px;
  font-weight: 400;
  line-height: 1;
  margin: 20px;
  padding: 12px 25px;
  text-decoration: none;
  text-align: center;
  text-transform: uppercase;
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
}

.btn-register {
  appearance: none;
  background-color: #E53F36;
  border: 2px solid #E53F36;
  border-radius: 20px;
  color: white;
  cursor: pointer;
  display: flex;
  align-self: center;
  font-size: 16px;
  font-weight: 400;
  line-height: 1;
  margin: 20px;
  padding: 12px 25px;
  text-decoration: none;
  text-align: center;
  text-transform: uppercase;
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
}

.card-order {
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 1200px;
    border-radius: 10px;
    box-shadow: 0 0 15px black;
    gap: 12px;
    position: absolute;
    top: 900px;
    background: #FFF;
}

.product-request-title {
    color: #F9CB32;
}

.image {
    width: 20px;
    height: 20px;
    padding: 10px 20px;
}
@media(max-width: 450px) {
.card-form{
    top: 80px;
}
}
@media(max-width: 700px) {
.card-form{

}
}

</style>
