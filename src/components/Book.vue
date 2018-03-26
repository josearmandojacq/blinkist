<template>

  <v-layout row wrap>
    <v-flex xs6>
      <v-card v-bind:class="{hide: added, 'book-container': !added}">
        <v-card-media :src='book.image' height='100px'>
        </v-card-media>
        <v-card-title primary-title>
          <div>
            <h3 class='headline mb-0'>{{book.name}}</h3>
            <div>{{book.author}}</div>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn flat color='orange' v-on:click='addToCurrently' v-bind:class='{hide: toogleBooksButtons}'>+ Add to Library</v-btn>
          <v-btn flat color='orange' v-on:click='removeBook' v-bind:class='{hide: !toogleBooksButtons}'>Remove</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  name: 'Book',
  props: {
    book: Object,
    addSelectedBooks: Function,
    removeSelectedBook: Function,
    toogleBooksButtons: Boolean,
  },
  
  data() {
    return{
     added: false
    }
  },
  methods: {
    
    addToCurrently: function () {
      this.addSelectedBooks(this.book);
      this.added = true;
    },
    
    removeBook: function () {
      this.removeSelectedBook(this.book)
  
    },

  },
  
  
};
</script>

<style scoped>
  .book-container{
    width: 200px;
    
  }

  .hide{
    display: none;
  }
</style>
