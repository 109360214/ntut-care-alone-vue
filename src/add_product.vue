<template>
  <div id="app">
    <form @submit.prevent="addProduct">
      <h1>Product Name</h1>
      <input type='text' v-model="name">
      <h1>Product image_url</h1>
      <input type='url' v-model="imageUrl">
      <button type='submit'>Submit</button>
    </form>
  </div>

  <div>
    <select_product />
  </div>
</template>

<script>
import axios from 'axios'
import select_product from './select_product.vue'


  export default {
    name: 'MyComponent',
  components: { select_product },
    data() {
      return {
        name: '',
        imageUrl: ''
      }
    },
    methods: {
      addProduct() {
        const formData = new FormData()
        formData.append('name', this.name)
        formData.append('image_url', this.imageUrl)
        axios.post('add_product', formData)
          .then(response => {
            console.log(response.data)
            // 成功處理響應的代碼
          })
          .catch(error => {
            console.log(error)
            // 處理錯誤的代碼
          })
      }
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
