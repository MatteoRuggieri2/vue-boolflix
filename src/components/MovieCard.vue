<template>
    <div class="movie-card">

        <!-- Single Movie -->
        <ul >

            <!-- Titles -->
            <li>{{ singleMovie.title || singleMovie.name }}</li>
            <li>{{ singleMovie.original_title || singleMovie.original_name }}</li>
            
            <!-- Flag -->
            <li v-if="flagImgFounder()">
                <div class="flag-container">
                    <img :src="require('../assets/img/' + singleMovie.original_language + '.png')" :alt="singleMovie.original_language + ' flag'">
                </div>
            </li>
            <li v-else>{{ singleMovie.original_language }}</li>

            <!-- Vote -->
            <li>{{ singleMovie.vote_average }}</li>
        </ul>

    </div>
</template>

<script>
export default {
    name: 'MovieCard',
    props: {
        singleMovie: Object
    },
    data: function() {
        return {
            flagsPathArray: [ 'it.png', 'en.png', 'fr.png' ],
        }
    },
    methods: {
        flagImgFounder: function() {
            if(this.flagsPathArray.includes(this.singleMovie.original_language + '.png')) {
                return true;
            } else {
                return false;
            }
            
        },
    }
}
</script>

<style lang="scss" scoped>

    .movie-card {

        ul {
            border: 3px solid darkcyan;
            
            li {
                color: white;

                .flag-container {
                    width: 50px;
                }
            }
        }
    }
</style>