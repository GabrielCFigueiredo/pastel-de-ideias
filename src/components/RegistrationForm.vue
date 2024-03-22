<template>
<div class="card-form">
    <form class="form-card-group" @submit.prevent="submitForm">
        <div class="card-title">
            <h3>Monte aqui seu cardápio. O que está esperando?</h3>
        </div>
        <div class="card">
        <div class="card-input">
            <input class="title-product" type="text" placeholder="Titúlo do Pedido" v-model="nome" required />
            <input class="flavor-product" type="text" placeholder="Sabor" v-model="sabor" required />
            <input class="price-product" type="number" placeholder="R$" v-model="price" required />
        </div>
        <div class="card-description">
            <textarea class="description"  placeholder="Descrição" v-model="name" required></textarea>
        </div>
        <div class="card-preview">
            <div class="image-preview" :style="{'background-image': `url(${previewImage})`}" @click="selectImage"></div>
            <input ref="fileInput" type="file" @input='pickFile'>
        </div>
        <br>
        <br>
        <div class="card-button">
            <div>
                <button class="btn-cancel">Cancelar</button>
            </div>
            <div>
                <button class="btn-register">Cadastrar</button>
            </div>
        </div>
        <div>
            <img class="pastries" src="../../public/pastel.png" alt="">
        </div>
    </div>
    </form>
</div>
</template>
<script>
export default {
  name: 'RegistrationForm',
  data () {
    return {
      nome: '',
      sabor: '',
      price: '',
      previewImage: null
    }
  },
  methods: {
    submitForm () {
      console.log(
        this.nome,
        this.sabor,
        this.price
      )
    },
    selectImage () {
      this.$refs.fileInput.click()
    },
    pickFile () {
      const input = this.$refs.fileInput
      const file = input.files
      if (file && file[0]) {
        const reader = new FileReader()
        reader.onload = e => {
          this.previewImage = e.target.result
        }
        reader.readAsDataURL(file[0])
        this.$emit('input', file[0])
      }
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

.form-card-group {
    display: flex;
    flex-direction: column;
    width: 50%;
    align-items: center;
    box-shadow: 0 0 15px black;
    border-radius: 10px;
    position: absolute;
    top: 25%;
    background-color: white;
}
.card-input {
    display: flex;
    gap: 2%;
    width: 100%;
    padding: 1%;
}

.title-product {
    width: 90%;
    padding: 1%;
}

.price-product {
    width: 20%;
    padding: 1%;
}

.flavor-product {
    width: 90%;
    padding: 1%;
}

.card-description {
    width: 100%;
    padding: 2%;
}

.description {
    width: 99%;
    height: 30%;
}

.description::placeholder {
    padding: 1%;
}

.card-preview {
    width: 100%;
    height: 20vh;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.image-preview {
    width: 100%;
    height: 70%;
    display: block;
    cursor: pointer;
    margin: 0 auto 10px;
    background-size: cover;
    background-position: center center;
    border: 1px solid #E53F36;
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
.btn-cancel:hover {
    box-shadow: 0 0 10px 0 blue inset, 0 0 10px 4px blue;
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

.btn-register:hover {
    box-shadow: 0 0 10px 0 blue inset, 0 0 10px 4px blue;
  }

.card-button {
    display: flex;
    position: absolute;
    top: 91%;
}
.pastries {
    position: absolute;
    top: 0;
    color: transparent;
}
</style>
