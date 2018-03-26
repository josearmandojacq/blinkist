<template>
  <div>
  <header>
    <h1>{{title}}</h1>
    <div class='library-separator color'></div>
  </header>
  
  <!-- List all of books added to the library/reading now -->
  <div class="states-container spacing">
    <h3 v-bind:class="{color: addedBooks.length >= 1}">Currently reading</h3>
    <div class='currently-separator color'></div>
    <v-container grid-list-md text-xs-center class="margin" >
      <v-layout row wrap >
        <v-flex xs4 v-for="book in addedBooks" v-bind:key="book._id">
          <Book :book='book' :removeSelectedBook='removeSelectedBook.bind(this)' :toogleBooksButtons="toogleBooksButtons"/>
        </v-flex>
      </v-layout>
    </v-container>
    </div>

  <!-- List all of books -->
    <div id="books-container">
      <h2>You might like</h2>
      <h3>The community's more read title</h3>
      <v-container grid-list-md text-xs-center class="margin" >
        <v-layout row wrap >
          <v-flex xs4 v-for="book in books" v-bind:key="book._id">
            <Book :book="book"  :addSelectedBooks="addSelectedBooks.bind(this)" />
          </v-flex>
        </v-layout >
      </v-container>
    </div>
</div>
</template>

<script>
import Data from '../assets/data.json';
import Book from './Book';


export default {
  name: 'Library',
  components:{
    Book
  },
  data() {
    return {
      title: 'Library',
      addedBooks: [],
      finishedBooks: [],
      books: Data,
      toogleBooksButtons: false,
    };
  },
  methods: {
    //Add the selected book to currently reading
    addSelectedBooks: function (book) {
      const newBook = book;
      this.addedBooks.push(newBook);
      this.toogleBooksButtons= true;
    },
    //add the selected book to finished
    removeSelectedBook: function (book) {
      this.addedBooks.splice(this.addedBooks.indexOf(book), 1);
      const removedBook = book;
      this.finishedBooks.push(removedBook);
      
    }
  },
  
};
</script>

<style scoped>
header > h1{
  margin: 0 0 20px 5%;
}
.library-separator {
  width: 90%;
  height: 2px;
  background-color: #83DF85;
  margin: 0 auto;
}
.color{
  color: #74C775;
}
.currently-separator{
  width: 20%;
  height: 2px;
  background-color: #83DF85;
}
.states-container{
  margin: 0 0 30px 5%;
}

#books-container{
  margin-left: 5%;
}

div.states-container.spacing > h3{
  width: 200px;
  margin-top: 30px;
}

.margin{
  margin: 20px 0 0 0;
}
</style>
