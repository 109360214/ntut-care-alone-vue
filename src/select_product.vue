<template>
    <div>
      <form @submit.prevent="send">
        <div v-for="(item, index) in items" :key="index">
          <h1>產品名稱 : {{ item.name }}</h1>
          <img :src="item.image_url" height="200" width="200"><br>
          <label>
            <input type="checkbox" v-model="selectedItems" :value="item.name" :data-image="item.image_url"><br>
          </label>
        </div>
        <button type="submit" style="width: 160px; height: 50px;">確認送出</button>
      </form>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      items: [],
      selectedItems: []
    }
  },
  methods: {
    send() {
      const formData = new FormData()
      formData.append('selectedItems', this.selectedItems)
      axios.post('select_product', formData)
        .then(response => {
          console.log(response.data)
          // 成功處理響應的代碼
        })
        .catch(error => {
          console.log(error)
          // 處理錯誤的代碼
        })
    }
  },
  mounted() {
    axios.get('http://localhost:3000/products')
      .then(response => {
        this.items = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>