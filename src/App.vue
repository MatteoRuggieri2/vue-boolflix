<template>
  <div id="app">
    <Header @getUserText="search" />
    <Main :apiFilmObjects="moviesArray" :apiTvSeriesObjects="tvSeriesArray" />
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
      apiKey: '594f744473899f8902a8ed104f7d9a22',
      userSearchText: '',
      moviesArray: [],
      tvSeriesArray: []
    }
  },
  methods: {
    search: function(userText) {
      this.userSearchText = userText;
      this.searchedMovies();
      this.searchedSeriesTv();
    },

    // Chiamata API per i film
    searchedMovies: function() {
      if(this.userSearchText.length > 0) {
        axios.get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: this.apiKey,
            query: this.userSearchText
          }
        })
        .then((response) => {
          this.moviesArray = response.data.results;
        });
      }

    },

    // Chiamata API per le serie TV
    searchedSeriesTv: function() {
      if(this.userSearchText.length > 0) {
        axios.get('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: this.apiKey,
            query: this.userSearchText
          }
        })
        .then((response) => {
          this.tvSeriesArray = response.data.results;
        });
      }

    }
  },
  created: function() {
    // Chiamata API per i film consigliati
    axios.get('https://api.themoviedb.org/3/discover/movie', {
      params: {
        api_key: this.apiKey
      }
    })
    .then((response) => {
      this.moviesArray = response.data.results;
    });

    // Chiamata API per le serie TV consigliate
    axios.get('https://api.themoviedb.org/3/discover/tv', {
      params: {
        api_key: this.apiKey
      }
    })
    .then((response) => {
      this.tvSeriesArray = response.data.results;
    });
  }
};
</script>

<style lang="scss">
@import './style/general.scss';

</style>
