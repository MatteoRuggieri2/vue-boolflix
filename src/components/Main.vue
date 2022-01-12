<template>
    <main>
        <div class="wrapper">

            <!-- Films -->
            <div class="films-container">
                <h2>Film</h2>
                <MovieCard v-for="(movie, index) in apiFilmObjects" :key="index" :singleMovie="movie" />
            </div>

            <!-- Series TV -->
            <div class="series-container">
                <h2>Serie TV</h2>
                <MovieCard v-for="(series, index) in apiTvSeriesObjects" :key="index" :singleMovie="series" />
            </div>
        </div>
    </main>
</template>

<script>

import MovieCard from "./MovieCard.vue";

export default {
    name: 'Main',
    components: {
        MovieCard,
    },
    props: {
        apiFilmObjects: Array,
        apiTvSeriesObjects: Array
    }
}
</script>

<style lang="scss" scoped>
    main {
        height: calc(100vh - 60px);
        background-color: rgb(44, 44, 44);
        color: white;
        overflow-y: auto;

        .wrapper {

            .films-container {
                border: 3px solid red;
            }

            .series-container {
                border: 3px solid yellow;
            }
        }
    }
</style>