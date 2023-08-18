<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const books = ref([]);


async function getBooks() {
  try {
    const response = await axios.get("https://www.dbooks.org/api/recent");
    books.value = response.data.books;
    console.log(books.value);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

onMounted(async () => {
  await getBooks();
});
</script>
<template>
<div>
    <ul class="book-list">
      <li v-for="book in books" :key="book.id" class="book-item">
        <h2>{{ book.title }}</h2>
        <p>Authors: {{ book.authors }}</p>
        <img :src="book.image" alt="Book Cover" />
        <a :href="book.url" target="_blank">Read More</a>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.book-list {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
}

.book-item {
  width: calc(33.33% - 20px); /* Adjust as needed */
  margin: 10px;
  padding: 15px;
  border: 1px solid #ccc;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
}
@media (max-width: 768px) {
  .book-item {
    width: calc(80% - -25px); /* Adjust as needed */
  }
}
</style>
