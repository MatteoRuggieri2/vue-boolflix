<template>
    <div class="movie-card">

        <!-- Single Movie -->
        <ul >
            <li>{{ singleMovie.title }}</li>
            <li>{{ singleMovie.original_title }}</li>
            <li>{{ singleMovie.original_language }}</li>
            <li>{{ singleMovie.vote_average }}</li>
        </ul>

    </div>
</template>

<script>
export default {
    name: 'MovieCard',
    props: {
        singleMovie: Object
    }
}
</script>

<style lang="scss" scoped>

    .movie-card {

        ul {
            border: 3px solid darkcyan;
            
            li {
                color: white;
            }
        }
    }
</style>