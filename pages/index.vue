<template>
  <div>
    <NavigasiComponent />
    <h1 class="flex items-center text-5xl font-extrabold ms-3">Beranda</h1>
    <div v-if="error" class="error">{{ error }}</div>
    <div v-if="articles.length === 0" class="loading">Loading...</div>
    <div v-else class="articles">
      <CardComponent v-for="article in articles" :key="article.id" :article="article" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import CardComponent from '~/components/CardComponent.vue'

const articles = ref([])
const error = ref(null)

onMounted(async () => {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/posts')
    articles.value = response.data
  } catch (err) {
    error.value = 'Error fetching articles'
  }
})
</script>

<style scoped>
.articles {
  display: flex;
  flex-wrap: wrap;
}
.article-card {
  border: 1px solid #eaeaea;
  border-radius: 5px;
  padding: 16px;
  margin: 16px;
  width: calc(33.333% - 32px);
  box-sizing: border-box;
}
.error {
  color: red;
}
.loading {
  text-align: center;
}
</style>
