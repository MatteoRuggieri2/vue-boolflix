<template>

    <!-- Single Movie -->
    <div @mouseenter="getCast()" class="movie-card">

        <!-- Poster -->
        <div v-if="(singleMovie.poster_path !== null)" class="poster">
            <img :src="'https://image.tmdb.org/t/p/w342/' + singleMovie.poster_path" :alt="'Poster ' + singleMovie.title || singleMovie.name">
        </div>

        <div v-else class="poster-not-found">
            <img src="../assets/img/img-notfound.jpg" alt="Poster not found">
            <div class="movie-title">{{ singleMovie.title || singleMovie.name }}</div>
        </div>

        <MovieInfo :singleMovieObject="singleMovie" :cast="castArray" :genres="movieGenres" />

    </div>
</template>

<script>

import axios from 'axios';
import MovieInfo from "./MovieInfo.vue";

export default {
    name: 'MovieCard',
    components: {
        MovieInfo,
    },
    props: {
        singleMovie: Object,
        type: String
    },
    data: function() {
        return {
            castArray: [],
            movieGenres: [],
            apiKey: '594f744473899f8902a8ed104f7d9a22'
        }
    },
    methods: {
        
        // Questa funzione serve a prendere gli attori e i generi dei film e delle serie TV
        getCast: function() {

            // Chiamata API per gli attori dei film
            axios.get(`https://api.themoviedb.org/3/${this.type}/${this.singleMovie.id}/credits`, {
                params: {
                api_key: this.apiKey,
                language: "it"
                }
            })
            .then((response) => {
                this.castArray = response.data.cast;
            });

            // Chiamata API per il genere dei film e delle serie
            axios.get(`https://api.themoviedb.org/3/${this.type}/${this.singleMovie.id}`, {
                params: {
                api_key: this.apiKey
                }
            })
            .then((response) => {
                this.movieGenres = response.data.genres;
            });
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/variables.scss';

    .movie-card {
        width: 13vW;
        flex-shrink: 0;
        position: relative;
        overflow-y: auto;
        background-color: black;
        border: 1px solid black;

        .poster {
            max-width: 100%;
        }

        .poster-not-found {
            max-width: 100%;
            position: relative;

            .movie-title {
                width: 12vW;
                max-width: 12vW;
                padding: 5px 10px 2px;
                position: absolute;
                top: 20px;
                left: 50%;
                transform: translateX(-50%);
                background-color: rgba(0, 0, 0, 0.7);
                font-family: $title_text_font;
                text-transform: uppercase;
                text-align: center;
            }
        }

        &:hover .poster,
        &:hover .poster-not-found {
            filter: brightness(0.1);
        }

        &:hover .movie-info {
            display: block;
        }
    }
</style>