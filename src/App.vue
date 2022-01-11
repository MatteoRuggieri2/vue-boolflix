<template>
  <div id="app">
    <Header @getUserText="searchedMovies" />
    <Main :apiObjects="moviesArray" />
  </div>
</template>

<script>

import axios from 'axios';
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data: function() {
    return {
      userSearchText: '',
      moviesArray: []
    }
  },
  methods: {
    searchedMovies: function(userText) {
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: '594f744473899f8902a8ed104f7d9a22',
          query: userText
        }
      })
      .then((response) => {
        this.moviesArray = response.data.results;
      });

      this.userSearchText = userText;
    }
  }
};
</script>

<style lang="scss">
@import './style/general.scss';

</style>
