<template>
    <div class="movie-info">
        <ul>

            <!-- Titles -->
            <li>Titolo: {{ singleMovieObject.title || singleMovieObject.name }}</li>
            <li>Titolo originale: {{ singleMovieObject.original_title || singleMovieObject.original_name }}</li>
            
            <!-- Flag -->
            <li v-if="flagImgFounder()">
                <span>Language: </span>
                <span class="flag-container">
                    <img :src="require('../assets/img/' + singleMovieObject.original_language + '.png')" :alt="singleMovieObject.original_language + ' flag'">
                </span>
            </li>
            <li v-else>{{ singleMovieObject.original_language }}</li>

            <!-- Vote -->
            <li>{{ fullStars }}</li>
            <li>
                <span>Voto: </span>
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
            flagsPathArray: [ 'it', 'en', 'fr' ],
            fullStars: this.numberOfStars(this.singleMovieObject.vote_average)
        }
    },
    methods: {
        flagImgFounder: function() {
            if(this.flagsPathArray.includes(this.singleMovieObject.original_language)) {
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
        display: none;
        padding: 40px 20px;
        position: absolute;
        top: 0;
        left: 0;

        ul {
            list-style-type: none;
            
            li {
                color: white;

                .flag-container {
                    display: inline-block;
                    width: 30px;
                }
            }
        }
    }

</style>