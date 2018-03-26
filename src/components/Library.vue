<template>
  <div>
  <header>
    <h1>{{title}}</h1>
    <div class='library-separator'></div>
  </header>

  <v-container class="states-container">
    <v-flex class="spacing">
      <h3>Currently reading</h3>
      <div v-for="book in addedBooks" v-bind:key="book._id">
        <Book :book='book' :removeSelectedBook='removeSelectedBook.bind(this)' :toogleBooksButtons="toogleBooksButtons"/>
      </div>
    </v-flex>

    <v-flex class="spacing">
      <h3>Finished</h3>
      <div v-for="book in finishedBooks" v-bind:key="book._id">
        <Book :book='book'/>
      </div>
    </v-flex>
  </v-container>

  <div id="books-container">
    <h2>You might like</h2>
    <h3>The community's more read title</h3>
    <div>
      <v-container grid-list-md text-xs-center>
    <div v-for="book in books" v-bind:key="book._id">
      <Book :book="book"  :addSelectedBooks="addSelectedBooks.bind(this)" />
    </div>
    </v-container>
    </div>
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
  margin: 0 0 30px 5%;
}
.library-separator {
  width: 90%;
  height: 2px;
  background-color: #A5CBA2;
  margin: 0 auto;
}
.states-container{
  display: flex;
  margin: 0 0 30px 5%;

}
.spacing{
  margin-bottom: 30px;
}
#books-container{
  margin-left: 5%;
}
</style>
