<template>
    <main>
        <div class="wrapper">

            <!-- Films -->
            <h2>FILM</h2>
            <div class="films-container">
                <MovieCard v-for="(movie, index) in apiFilmObjects" :key="index" :singleMovie="movie" type="movie"/>
            </div>

            <!-- Series TV -->
            <h2>SERIE TV</h2>
            <div class="series-container">
                <MovieCard v-for="(series, index) in apiTvSeriesObjects" :key="index" :singleMovie="series" type="tv" />
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
@import '../style/variables.scss';

    main {
        height: calc(100vh - 60px);
        padding-left: 20px;
        background-color: rgb(44, 44, 44);
        color: $primary_text_color;
        overflow-y: auto;

        .wrapper {

            h2 {
                margin: 8px 0;
                font-family: $title_text_font;
                font-size: 24px;
                font-weight: 800;
            }

            .films-container,
            .series-container {
                display: flex;
                overflow-x: auto;
                padding-right: 20px;
            }
        }
    }
</style>