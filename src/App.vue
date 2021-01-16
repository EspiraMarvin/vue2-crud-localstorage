<template>
  <div id="app">
    <AddBookItem v-on:add-book-event="addBookItem" v-on:edit-book-event="editBookItemEvent" v-bind:editBook="editBook"/>
    <div>
      <Books v-bind:books="books" v-on:del-book-event="deleteBookItem" v-on:edit-book-event="editBookItem" />
    </div>
  </div>
</template>

<script>
  import Books from "./components/Books";
  import AddBookItem from "./components/AddBookItem";

export default {
  name: 'App',
  components: {
    Books,
    AddBookItem
  },
  data () {
    return {
      books: [],
      editBook: {
        title: '',
        id: ''
      }
    }
  },
  methods: {
    addBookItem(newBook){
      // console.log('newbook', newBook.title);
        this.books = [...this.books, newBook];
      // this.books.unshift(newBook)
    },
    deleteBookItem(id){
      this.books = this.books.filter(book => book.id !== id);
    },
    editBookItem(id){
      //find the index of the book's id
      let objIndex = this.books.findIndex(obj=> obj.id === id);
      this.editBook.title = this.books[objIndex].title;
      this.editBook.id = id;
    },
    editBookItemEvent(bookItem){
      //find the index of this id's object
      let objIndex = this.books.findIndex(obj => obj.id === bookItem.id)
      //update the item
      this.books[objIndex].title = bookItem.title;
    }
  },
  watch: {
    books: {
      handler() {
        localStorage.setItem('books',JSON.stringify(this.books))
      },
      deep: true
    }
  },
  mounted() {
    if (localStorage.getItem("books")){
      this.books = JSON.parse(localStorage.getItem("books"))
    }
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
