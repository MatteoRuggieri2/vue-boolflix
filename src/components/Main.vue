<template>
    <main>
        <div class="wrapper">

            <!-- Films -->
            <MovieCard v-for="(movie, index) in apiObjects" :key="index" :singleMovie="movie" />

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
        apiObjects: Array
    }
}
</script>

<style lang="scss" scoped>
    main {
        height: calc(100vh - 60px);
        background-color: rgb(44, 44, 44);
        color: white;
        overflow-y: auto;
    }
</style>