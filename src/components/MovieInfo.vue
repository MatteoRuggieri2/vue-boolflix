<template>
    <div class="movie-info">
        <ul>

            <!-- Titles -->
            <li><span class="info-title">Titolo: </span>{{ singleMovieObject.title || singleMovieObject.name }}</li>
            <li v-if="filmTitleComparison() || seriesNameComparison()"><span class="info-title">Titolo originale: </span>{{ singleMovieObject.original_title || singleMovieObject.original_name }}</li>
            
            <!-- Flag -->
            <li v-if="flagImgFounder()">
                <span class="info-title">Language: </span>
                <span class="flag-container">
                    <img :src="require('../assets/img/' + singleMovieObject.original_language + '.png')" :alt="singleMovieObject.original_language + ' flag'">
                </span>
            </li>
            <li v-else>{{ singleMovieObject.original_language }}</li>

            <!-- Vote -->
            <li>
                <span class="info-title">Voto: </span>
                <span class="stars-container"> 
                    <span v-for="(number, index) in 5" :key="index">
                        <span v-if="(number <= fullStars)" class="full-star-icon"><i class="fas fa-star"></i></span>
                        <span v-else class="empty-star-icon"><i class="far fa-star"></i></span>
                    </span>
                </span>
            </li>

            <!-- Cast -->
            <li>
                <span class="info-title">Attori: </span>
                <span v-for="(people, index) in cast" :key="people.id">
                    <span v-if="(index < 4)">{{ people.name }}, </span>
                    <span v-else-if="(index === 4)">{{ people.name }} ...</span>
                </span>
            </li>

            <!-- Overview -->
            <li>
                <span class="info-title">Trama: </span>
                <span v-if="(singleMovieObject.overview.length > 0)">{{ singleMovieObject.overview }}</span>
                <span v-else>Non disponibile</span>
            </li>

        </ul>
    </div>
</template>

<script>
export default {
    name: 'MovieInfo',
    props: {
        singleMovieObject: Object,
        cast: Array
    },
    data: function() {
        return {
            flagsPathArray: [ 'it', 'en', 'fr' ],
            fullStars: this.numberOfStars(this.singleMovieObject.vote_average)      // Numero di stelle piene
        }
    },
    methods: {

        // Questa funzione serve a verificare se è disponibile l'immagine della bandiera.
        // return: true se è disponibile.
        flagImgFounder: function() {
            if(this.flagsPathArray.includes(this.singleMovieObject.original_language)) {
                return true;
            } else {
                return false;
            }
            
        },

        // Questa funzione serve a verificare quante sono le stelle piene.
        // Arrotonda per difetto (< 0.5) e per eccesso (> 0.5).
        // agomento: Numero decimale da 1 a 10.
        // return: ritorna il numero di stelle piene.
        numberOfStars: function(decimalVote) {
            const stars = decimalVote / 2
            
            return Math.round(stars);
        },

        // Questa funzione serve a verificare quante sono le stelle vuote.
        // agomento: Numero intero di stelle da 1 a 5.
        // return: ritorna il numero di stelle vuote.
        numberOfEmptyStars: function(numberOfStars) {
            const emptyStars = 5 - numberOfStars
            
            return emptyStars;
        },

        // Questa funzione serve a verificare se il titolo del film è diverso dal
        // titolo originale.
        // return: true se è diverso, e quindi deve stamparlo.
        filmTitleComparison: function() {
            if(this.singleMovieObject.original_title !== this.singleMovieObject.title) {
                return true;
            } else {
                return false;
            }
        },

        // Questa funzione serve a verificare se il nome della serie TV è diverso dal
        // nome originale.
        // return: true se è diverso, e quindi deve stamparlo.
        seriesNameComparison: function() {
            if(this.singleMovieObject.original_name !== this.singleMovieObject.name) {
                return true;
            } else {
                return false;
            }
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

                .stars-container {
                    display: inline-block;
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