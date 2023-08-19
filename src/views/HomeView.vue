<script setup>
import SearchBar from "../components/SearchBar.vue";
import BookList from "../components/BookList.vue";
import { onMounted, ref } from "vue";
import axios from "axios";

const books = ref();
const filteredBooks = ref();

function filter(keyword) {
  filteredBooks.value = books.value.filter((v) => {
    var title = v.title.toLowerCase();
    if (title.includes(keyword.toLowerCase())) {
      return v;
    }
  });
}

async function getBooks() {
  try {
    const response = await axios.get("https://www.dbooks.org/api/recent");
    books.value = response.data.books;
    filteredBooks.value = books.value;
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
  <div class="home">
    <SearchBar @search="filter" />
    <BookList :books="filteredBooks" />
  </div>
</template>
