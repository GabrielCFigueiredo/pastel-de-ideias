<template>
<div class="card-form">
    <form class="form-card-group" @submit.prevent="submitForm">
        <div class="card-title">
            <h3>Monte aqui seu cardápio. O que está esperando?</h3>
            <input type="checkbox" v-model="isChecked" />
        </div>
        <div class="card-pastries">
            <img class="pastries" src="../../public/pastel.png" alt="">
        </div>
        <div class="card">
        <div class="card-input">
            <input class="title-product" type="text" placeholder="Titúlo do Pedido" v-model="name" required minlength="3" maxlength="60" />
            <input class="flavor-product" type="text" placeholder="Sabor" v-model="flavor" required minlength="3" maxlength="60" />
            <input class="price-product" type="number" placeholder="R$" v-model="price" required />
        </div>
        <div class="card-description">
            <textarea class="description"  placeholder="Descrição" v-model="description" required></textarea>
        </div>
        <div class="card-preview">
            <div class="image-preview" :style="{'background-image': `url(${previewImage})`}" @click="selectImage"></div>
            <input ref="fileInput" type="file" @input='pickFile'>
        </div>
        <br>
        <br>
        <div class="card-button">
            <div>
                <button class="btn-cancel" @click="cancelForm" type="submit">Cancelar</button>
            </div>
            <div>
                <button class="btn-register" type="submit">Cadastrar</button>
            </div>
        </div>
    </div>
    </form>
</div>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<div class="card-order"  v-for="product in reversedResult" :key="product">
    <div>
        <h1>Aqui está o seu pedidos Bom Apetite!</h1>
    </div>
    <div class="card-title-order">
        <div class="order">
            <h3 class="product-request-title">{{ product.name }}</h3>
            <h3 class="asking-price">R$ {{ product.price }}</h3>
        </div>
        <div>
        <h3>Sabor: {{ product.flavor }}</h3>
        <h3>Descrição: {{ product.description }}</h3>
        </div>
    </div>
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
.card-pastries {
    width: 100%;
}
.pastries {
    position: absolute;
    width: 50%;
    height: 85%;
    bottom: 65%;
    right: 80%;
    transform: rotate(10deg);
    filter: blur(4px);
}

.card-order {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    height: 30vh;
}
.card-title-order {
    width: 50%;
    height: 30%;
}
.order {
    display: flex;
    justify-content: space-between;
    background-color: #E53F36;
}

.product-request-title {
    color: #F9CB32;
}
.asking-price {
    color: #FFF;
}
</style>
