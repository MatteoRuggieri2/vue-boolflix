<template>
    <div class="movie-info">
        <ul>

            <!-- Titles -->
            <li><span class="info-title">Titolo: </span>{{ singleMovieObject.title || singleMovieObject.name }}</li>
            <li><span class="info-title">Titolo originale: </span>{{ singleMovieObject.original_title || singleMovieObject.original_name }}</li>
            
            <!-- Flag -->
            <li v-if="flagImgFounder()">
                <span class="info-title">Language: </span>
                <span class="flag-container">
                    <img :src="require('../assets/img/' + singleMovieObject.original_language + '.png')" :alt="singleMovieObject.original_language + ' flag'">
                </span>
            </li>
            <li v-else>{{ singleMovieObject.original_language }}</li>

            <!-- Vote -->
            <!-- <li>{{ fullStars }}</li> -->
            <li>
                <span class="info-title">Voto: </span>
                <span v-for="(number, index) in 5" :key="index">
                    <span v-if="(number <= fullStars)" class="full-star-icon"><i class="fas fa-star"></i></span>
                    <span v-else class="empty-star-icon"><i class="far fa-star"></i></span>
                </span>
            </li>

            <!-- Overview -->
            <li>
                <span class="info-title">Trama: </span>{{ singleMovieObject.overview }}
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
@import '../style/variables.scss';

    .movie-info {
        display: none;
        padding: 40px 20px;
        position: absolute;
        top: 0;
        left: 0;
        font-family: $primary_text_font;

        ul {
            list-style-type: none;
            
            li {
                color: white;
                font-size: 14px;

                .info-title {
                    // margin-right: 10px;
                    font-weight: bold;
                    font-size: 18px;
                }

                .flag-container {
                    display: inline-block;
                    width: 30px;
                }

                .full-star-icon {
                    color: orange;
                    cursor: pointer;
                }

                .empty-star-icon {
                    cursor: pointer;
                }
            }
        }
    }

</style>