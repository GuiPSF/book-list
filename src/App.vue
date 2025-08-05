<script setup>
import Books from './components/Books.vue';
import BookProgress from './components/BookProgress.vue';
import { reactive, ref } from 'vue'
import AddBook from './components/AddBook.vue';


 let books = reactive([
  
        {
          id: 1,
          title: "History of Europe",
          cover:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSR-wBLwiLL0uHCrzje6Th0KLhF4q7rDLR-lA&s",
          isRead: true,
          isbn: "0-395-07157-8",
          author: "Daniel Trejo",
        },
        {
          id: 2,
          title: "Penguin Classics",
          cover:
            "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQCQZacL1Ghd0fyH2MeRIJT0XOypTG_UMv0Ug&s",
          isRead: false,
          isbn: "0-395-07157-8",
          author: "Daniel Trejo, Jon Snow",
        },
        {
          id: 3,
          title: "Becoming",
          cover:
            "https://m.media-amazon.com/images/I/81cJTmFpG-L.jpg",
          isRead: false,
          isbn: "0-395-07157-8",
          author: "Daniel Trejo",
        },
        {
          id: 4,
          title: "Sonnets",
          cover:
            "https://m.media-amazon.com/images/I/715hva4FrAL._UF894,1000_QL80_.jpg",
          isRead: false,
          isbn: "0-395-07157-8",
          author: "Daniel Trejo",
        },
      
 ]);

 let showAddBook = ref(false);

function toggleIsRead(id) {
  books.forEach((book) => {
    if(book.id == id) {
      book.isRead = !book.isRead
    }
  })
}

  


function addBook(newBook) {
  newBook.id = Math.max(...books.map(el => el.id)) + 1;
  books.push(newBook);
  showAddBook.value = false;
}

</script>

<template>
  <div v-if="!showAddBook" class="container">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button
        class="btn"
        @click="showAddBook = true"
      >
        Adicionar Livro +
      </button>
    </div>
 
    <div class="books-container">
      <Books @toggleIsRead="toggleIsRead" :books="books" />
      <BookProgress :books="books"/>

    </div>
  </div>
  <div v-else class="container">
    <AddBook @addBook="addBook" @closeAddBook="showAddBook = false"/>
  </div>
</template>

<style scoped>

</style>
