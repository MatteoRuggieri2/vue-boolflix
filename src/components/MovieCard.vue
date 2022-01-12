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
        border: 3px solid darkcyan;

        .poster-not-found {
            width: 342px;
            height: 513px;

            img {
                width: 100%;
                height: 100%;
                object-fit: cover;
                object-position: center;
            }
        }
    }
</style>