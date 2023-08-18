<script setup>
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
import axios from "axios";

const route = useRoute();
const books = ref({}); 



async function getBook() {
   try {
      const response = await axios.get("https://www.dbooks.org/api/book/"+ route.params.id)
      books.value = response.data;
      console.log(books.value);
   } catch (error) {
    console.log(error);
   }
}


onMounted(()=>{
  getBook();
})
</script>

<template>
  <div class="card">
    <img :src="books.image" alt="Book Cover" class="book-image" />
    <div class="book-details">
      <h1>{{ books.title }}</h1>
      <h2>{{ books.subtitle }}</h2>
      <p>Author: {{ books.authors }}</p>
      <p>Publisher: {{ books.publisher }}</p>
      <p>Pages: {{ books.pages }}</p>
      <p>Year: {{ books.year }}</p>
      <p>{{ books.description }}</p>
      <a :href="books.url" target="_blank">View on dBooks</a>
      <a :href="books.download" target="_blank">Download</a>
    </div>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  border: 1px solid #ccc;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: 20px;
}

.book-image {
  width: 200px;
  height: auto;
  object-fit: cover;
}

.book-details {
  padding: 20px;
}

h1 {
  font-size: 24px;
  margin: 0 0 8px;
}

h2 {
  font-size: 18px;
  margin: 0 0 8px;
  color: #666;
}

p {
  margin: 8px 0;
  color: #444;
}

a {
  display: inline-block;
  margin-top: 10px;
  color: #007bff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
