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
            <li>{{ numberOfStars(singleMovieObject.vote_average) }}</li>
            <li>
                <span v-for="(number, index) in numberOfStars(singleMovieObject.vote_average)" :key="index + 10"><i class="fas fa-star"></i></span>
                <span v-for="(number, index) in numberOfEmptyStars(numberOfStars(singleMovieObject.vote_average))" :key="index + 20"><i class="far fa-star"></i></span>
                <!-- ATTENZIONE!  Il +10 e il +20 nella key, servono per avere numeri univoci, quindi non ripetuti tra di loro -->
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