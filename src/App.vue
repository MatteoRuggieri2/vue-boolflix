<template>
  <div id="app">
    <Header @getUserText="search" @backHome="backToHome" />
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

    // Questa funzione prende il testo scritto dall'utente attraverso l'emit (search) dall'header
    // e lo inserisce in una variabile all'interno dei data (userSearchText).
    // Successivamente avvia anche le funzioni che chiamano le API per i film e serie TV.
    // argomento: Ha bisogno del valore derivante dall'emit "search" dell'header.
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
            query: this.userSearchText,
            language: "it"
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
            query: this.userSearchText,
            language: "it"
          }
        })
        .then((response) => {
          this.tvSeriesArray = response.data.results;
        });
      }

    },

    // Chiamata API per i film e le serie TV consigliate (HOME)
    backToHome: function() {
      
      // Chiamata API per i film consigliati
      axios.get('https://api.themoviedb.org/3/discover/movie', {
        params: {
          api_key: this.apiKey,
          language: "it"
        }
      })
      .then((response) => {
        this.moviesArray = response.data.results;
      });

      // Chiamata API per le serie TV consigliate
      axios.get('https://api.themoviedb.org/3/discover/tv', {
        params: {
          api_key: this.apiKey,
          language: "it"
        }
      })
      .then((response) => {
        this.tvSeriesArray = response.data.results;
      });
    }
  },
  created: function() {
    this.backToHome()
  }
};
</script>

<style lang="scss">
@import './style/general.scss';

// Google Fonts
@import url('https://fonts.googleapis.com/css2?family=Martel+Sans:wght@300;600;800&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Mukta:wght@200;700&display=swap');

</style>
