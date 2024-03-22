<template>
<div class="container">
    <div class="card-form">
        <form class="form-card-group" @submit.prevent="submitForm">
            <header class="card-title">
                <h3>Monte aqui seu cardápio. O que está esperando?</h3>
            </header>
            <section class="card">
                <div class="card-input">
                    <input id="title-product" class="title-product" type="text" placeholder="Título do Pedido" v-model="name" required minlength="3" maxlength="60" />
                    <input id="flavor-product" class="flavor-product" type="text" placeholder="Sabor" v-model="flavor" required minlength="3" maxlength="60" />
                    <input id="price-product" class="price-product" type="number" placeholder="R$" v-model="price" required />
                </div>
                <div class="card-description">
                    <textarea id="description" class="description" placeholder="Descrição" v-model="description" required></textarea>
                </div>
                <div class="card-preview">
                    <div class="image-preview" :style="{'background-image': `url(${previewImage})`}" @click="selectImage"></div>
                    <input id="image-upload" ref="fileInput" type="file" @input='pickFile'>
                </div>
                <div class="card-pastries">
                    <img class="pastries" src="../../public/pastel.png" alt="">
                </div>
                <div class="card-button">
                    <button class="btn-cancel" @click="cancelForm" type="button">Cancelar</button>
                    <button class="btn-register" type="submit">Cadastrar</button>
                </div>
            </section>
        </form>
    </div>
    <section class="card-order" v-for="product in reversedResult" :key="product">
        <article class="card-title-order">
            <div>
                <h2 class="order-title">Aqui está o seu pedido. Bom Apetite!</h2>
            </div>
            <div class="order">
                <h3 class="product-request-title">{{ product.name }}</h3>
                <h3 class="asking-price">R$ {{ product.price }},00</h3>
            </div>
            <img class="image" :src='product.image' alt="suco">
            <div>
                <h3>Sabor: {{ product.flavor }}</h3>
                <h3>Descrição: {{ product.description }}</h3>
            </div>
        </article>
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
      image: '',
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
        description: this.description,
        image: this.image
      }
      this.result.push(data)
      this.clear()
      this.name = ''
      this.flavor = ''
      this.price = ''
      this.description = ''
      this.image = ''
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
.card-form {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
}

.card {
    display: flex;
    flex-direction: column;
    width: 95%;
    align-items: center;
    justify-content: center;
}

@media(max-width: 400px) {
.card {
    height: 20vh;
    padding: 10%;
}
}

h3 {
    color: #AD4925;
    padding: 0 3%;
}

.card-title {
    background-color: #F9CB32;
    width: 100%;
    padding: 0;
    border-radius: 10px 10px 0 0;
}

@media(max-width: 400px) {
.form-card-group {
    display: flex;
}
}
.card-input {
    display: flex;
    gap: 2%;
    width: 100%;
    padding: 1%;
}
@media (max-width: 400px) {
.card-input {
    flex-direction: column;
    align-items: center;
    height: 50%;
    gap: 10%;
    padding: 10%;
 }
}

.title-product {
    width: 95%;
    padding: 1%;
    border: 1px solid #A43C23;
}

@media (max-width: 400px) {
.title-product {
    flex-direction: column;
    align-items: center;
    height: 50%;
    width: 90%;
    gap: 10%;
 }
}
.title-product::placeholder {
    color: #A43C23;
}

.price-product {
    width: 20%;
    padding: 1%;
    border: 1px solid #A43C23;
}

.price-product::placeholder {
    color: #A43C23;
}

.flavor-product {
    width: 90%;
    padding: 1%;
    border: 1px solid #A43C23;
}

.flavor-product::placeholder {
    color: #A43C23;
}

.card-description {
    width: 100%;
    height: 20%;
    padding: 1%;
}

@media (max-width: 400px) {
.card-description {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 50%;
    gap: 10%;
    padding: 7% 0 0 0;
 }
}

.description {
    width: 99%;
    height: 50%;
    border: 1px solid #A43C23;
}

@media (max-width: 400px) {
.description {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 50%;
    width: 90%;
    gap: 10%;
 }
}
.description::placeholder {
    color: #A43C23;
}

.image-preview {
    width: 100%;
    height: 80%;
    display: block;
    cursor: pointer;
    background-size: cover;
    background-position: center center;
    border: 1px solid #A43C23;
}

@media(max-width: 400px) {
.image-preview {
    height: 90%;
    padding: 5% 0;
}
}

.card-pastries {
    width: 100%;
    height: 10vh;
}
.pastries {
    position: absolute;
    width: 50%;
    height: 85%;
    bottom: 55%;
    right: 80%;
    transform: rotate(10deg);
    filter: blur(4px);
}

.order {
    display: flex;
    justify-content: space-between;
    background-color: #E53F36;
}

@media(max-width: 400px) {
.order{
    width: 90vw;
    padding: 5% 0;
}
}

.asking-price {
    color: #FFF;
}

.form-card-group {
    display: flex;
    flex-direction: column;
    width: 50%;
    height: 50%;
    align-items: center;
    box-shadow: 0 0 15px black;
    border-radius: 10px;
    position: absolute;
    top: 25%;
    background-color: white;
}

@media(max-width: 400px) {
.form-card-group {
    width: 90%;
    top: 7%;
}
}

.card-preview {
    width: 100%;
    height: 20vh;
    display: flex;
    flex-direction: column;
    align-items: center;
}

@media(max-width: 400px) {
.card-preview {
    display: block;
    width: 90%;
}
}

.btn-cancel {
  box-sizing: border-box;
  appearance: none;
  background-color: #F9CB32;
  border: 2px solid #F9CB32;
  border-radius: 2em;
  color: #A43C23;
  cursor: pointer;
  display: flex;
  align-self: center;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1;
  margin: 20px;
  padding: 0.5em 1.0em;
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
  border-radius: 2em;
  color: white;
  cursor: pointer;
  display: flex;
  align-self: center;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1;
  margin: 20px;
  padding: 0.5em 1.0em;
  text-decoration: none;
  text-align: center;
  text-transform: uppercase;
  font-family: 'Montserrat', sans-serif;
  font-weight: 700;
}

@media(max-width: 400px) {
.btn-register {
    padding: 0.2em;
}
}

.card-button {
    display: flex;
    position: absolute;
    top: 91%;
}

.card-order {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: end;
    width: 100%;
    height: 30vh;
    padding: 10% 0;
}

@media(max-width: 400px) {
.card-order {

}
}

.product-request-title {
    color: #F9CB32;
}

.image {
    width: 20px;
    height: 20px;
}

@media(max-width: 400px) {
.card-title-order {
    width: 90%;
    height: 20vh;
    margin-top: 100%;
}
}

@media(max-width: 400px) {
.order-title {
    margin-top: 100%;
}
}
</style>
