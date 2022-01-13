<template>

    <!-- Single Movie -->
    <div class="movie-card">

        <!-- Poster -->
        <div v-if="(singleMovie.poster_path !== null)" class="poster">
            <img :src="'https://image.tmdb.org/t/p/w342/' + singleMovie.poster_path" :alt="'Poster ' + singleMovie.title || singleMovie.name">
        </div>

        <div v-else class="poster-not-found">
            <img src="../assets/img/img-notfound.jpg" alt="Poster not found">
        </div>

        <MovieInfo :singleMovieObject="singleMovie" />

    </div>
</template>

<script>

import MovieInfo from "./MovieInfo.vue";

export default {
    name: 'MovieCard',
    components: {
        MovieInfo,
    },
    props: {
        singleMovie: Object
    },
}
</script>

<style lang="scss" scoped>

    .movie-card {
        width: 13vW;
        flex-shrink: 0;
        position: relative;
        overflow-y: auto;
        background-color: black;
        border: 1px solid black;

        .poster,
        .poster-not-found {
            max-width: 100%;
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