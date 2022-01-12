<template>
    <div class="movie-info">
        <ul>

            <!-- Titles -->
            <li>{{ singleMovieObject.title || singleMovieObject.name }}</li>
            <li>{{ singleMovieObject.original_title || singleMovieObject.original_name }}</li>
            
            <!-- Flag -->
            <li v-if="flagImgFounder()">
                <div class="flag-container">
                    <img :src="require('../assets/img/' + singleMovieObject.original_language + '.png')" :alt="singleMovieObject.original_language + ' flag'">
                </div>
            </li>
            <li v-else>{{ singleMovieObject.original_language }}</li>

            <!-- Vote -->
            <li>{{ fullStars }}</li>
            <li>
                <span v-for="(number, index) in 5" :key="index">
                    <span v-if="(number <= fullStars)"><i class="fas fa-star"></i></span>
                    <span v-else><i class="far fa-star"></i></span>
                </span>
            </li>

        </ul>
    </div>
</template>

<script>
export default {
    name: 'MovieInfo',
    props: {
        singleMovieObject: Object
    },
    data: function() {
        return {
            flagsPathArray: [ 'it.png', 'en.png', 'fr.png' ],
            fullStars: this.numberOfStars(this.singleMovieObject.vote_average)   // ex. 4
        }
    },
    methods: {
        flagImgFounder: function() {
            if(this.flagsPathArray.includes(this.singleMovieObject.original_language + '.png')) {
                return true;
            } else {
                return false;
            }
            
        },

        numberOfStars: function(decimalVote) {
            const stars = decimalVote / 2
            
            return Math.round(stars);
        },

        numberOfEmptyStars: function(numberOfStars) {
            const emptyStars = 5 - numberOfStars
            
            return emptyStars;
        }
    }
}
</script>

<style lang="scss" scoped>

    .movie-info {

        ul {
            
            li {
                color: white;

                .flag-container {
                    width: 50px;
                }
            }
        }
    }

</style>