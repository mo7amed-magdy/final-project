<template>
<div class="text-white flex justify-center text-7xl mb-4">
  <h1>Welcome to Our Library</h1>
</div>


<div class="wrapper active-popup ">
<Header 
:showAddBook="showAddBook"
:showBooks="showBooks"
:Searchbook="showSearchBook"
@toggle-show-books="ToggleShowBooks"
@toggle-add-book="ToggleAddBook"
@toggle-search-books="ToggleSearchBook"
title="Books" />

<div v-show="showSearchBook">
  <Searchbook @search-book="searchBook"/>
</div>


<div v-show="showAddBook">
    <Addbook @add-book="addBook" />
</div>

<div v-show="searched">
<Book 

@delete-book="deletebook" :book = "book" />

</div>

<div v-show="showBooks">
    <Books 
    @toggle-update="Toggleupdate"
    @update-book="getBookid"
    @delete-book="deletebook" :books="books" />
</div>
<div v-show="showupdate">
<Update 
@add-book="Updatebook"
:id="uid"/>
</div>


</div>
</template>

<script>
import Header from "./components/Header.vue"
import Books from "./components/Books.vue"
import Addbook from "./components/Addbook.vue"
import Searchbook from "./components/Searchbook.vue"
import Book from "./components/Book.vue"
import Update from "./components/Update.vue"

export default{
    name: 'App',
    components: {
        Header,
        Books,
        Addbook,
        Searchbook,
        Book,
        Update
    },
    data(){
        return{
            books: [],
            showAddBook: false,
            showBooks: true,
            showSearchBook: false,
            searched:false,
            book: {},
            uid:0 ,
            showupdate:false,
        }
    },
    methods:{
      ToggleSearchBook(){
        this.showSearchBook = !this.showSearchBook
         !this.showSearchBook? (this.searched = this.showSearchBook) : ''
      },
      getBookid(id){
        console.log(id);
        this.uid=id
      },
      async searchBook(title){
        console.log(title);
        const res = await fetch(`http://localhost:8000/book/${title.title}`)
        const data = await res.json()
        this.book = data
        this.searched =true
      },
      Toggleupdate(){
        this.showupdate = !this.showupdate
        
      },
        ToggleShowBooks(){
            this.showBooks = !this.showBooks
        },
        ToggleAddBook(){
            this.showAddBook = !this.showAddBook
        },
        async addBook(book){
          const res = await fetch('http://localhost:8000/book',{
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(book),
          })
          const data = await res.json()
          
          this.books= [...this.books, data]
        },
        async Updatebook(book){
          const res = await fetch(`http://localhost:8000/book/${this.uid}`,{
            method: 'PUT',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(book),
          })
          this.books = await this.fetchBooks()
        },
        async deletebook(id){
          if(confirm('Are You Sure?')){
              const res = await fetch(`http://localhost:8000/book/${id}`,{
                method: 'DELETE',
              })
              res.status === 204 ? (this.books = this.books.filter((book) => book.id !== id)) : alert('Error deleting book')
            }
      },
      async fetchBooks(){
        const res = await fetch('http://localhost:8000/book')
        const data = await res.json()
        console.log(data);
        return data
        
      },
      
    },
    async created(){
        this.books = await this.fetchBooks()
            
    },
}

</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  width: 500px;
  background-color: bisque;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.wrapper {
    position: relative;
    width: 1100px;
    min-height: 80vh;
    background: transparent;
    border: 2px solid rgba(225, 225, 225, .5);
    border-radius: 20px;
    backdrop-filter: blur(20px);
    box-shadow: 0 0 30px rgb(0, 0, 0, .5);
    /* display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden; */
    transform: scale(0);
    transition: transform .5s, height .2s ease;
}

.wrapper.active-popup {
    transform: scale(1);
}

</style>