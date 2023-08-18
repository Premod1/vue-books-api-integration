<script setup>
import axios from 'axios';
import { ref  } from 'vue';


const query = ref('');
const data = ref([]);


const handleInput = () => {
  searchBook(query.value); // Pass the query value as an argument
};

async function searchBook(queryValue) {
  try {
    const response = await axios.get(`https://www.dbooks.org/api/search/${queryValue}`);
    const allBooks = response.data.books;
    
    // Filter books based on title containing the query
    data.value = allBooks.filter(book => 
      book.title.toLowerCase().includes(queryValue.toLowerCase())
    );
    console.log(data.value);
  } catch (error) {
    console.log(error);
  }
}
</script>



<template>
  <main>
    <h1>Book API Intigrators</h1>
    <form @submit.prevent="searchBook">
        <input 
            type="text"
            placeholder="Search for an book"
            v-model="query"
            @input="handleInput"
        />
        <button class="btn btn-primary">Search</button>
    </form>

    
  </main>
</template>
<style scoped>
main {
    margin: 0 auto;
    max-width: 768px;
    padding: 1.5rem;
}
h1 {
    text-align: center;
    margin-bottom: 1.5rem;
}
form {
    display: flex;
    max-width: 480px;
    margin: 0 auto 1.5rem;
}
form input {
    appearance: none;
    outline: none;
    border: none;
    background: white;
    display: block;
    color: #888;
    font-size: 1.125rem;
    width: 100%;

    /* Add borders and rounded corners */
    border: 1px solid #ccc;
    border-radius: 4px;
}
button {
    appearance: none;
    cursor: pointer;
    display: block;
    padding: 0.5rem 1rem;
    font-size: 1.125rem;
    font-weight: 400;
    text-transform: uppercase;
}
</style>