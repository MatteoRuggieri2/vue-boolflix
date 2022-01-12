<template>

    <!-- Single Movie -->
    <div class="movie-card">

        <!-- Poster -->
        <div v-if="(singleMovie.poster_path !== null)" class="poster">
            <img :src="'https://image.tmdb.org/t/p/w342/' + singleMovie.poster_path" :alt="'Poster ' + singleMovie.title || singleMovie.name">
        </div>

        <div v-else class="poster-not-found">
            <img src="../assets/img/img-notfound.jpg" alt="Poster not found">
        </div>

        <!-- Movie Info -->
        <ul>

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
            <li>{{ numberOfStars(singleMovie.vote_average) }}</li>
            <li>
                <span v-for="(number, index) in numberOfStars(singleMovie.vote_average)" :key="index"><i class="fas fa-star"></i></span>
                <span v-for="(number, index) in numberOfEmptyStars(numberOfStars(singleMovie.vote_average))" :key="index"><i class="far fa-star"></i></span>
            </li>

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

    .movie-card {
        border: 3px solid darkcyan;

        .poster-not-found {
            width: 342px;
            height: 513px;

            img {
                width: 100%;
                height: 100%;
                object-fit: cover;
                object-position: center;
            }
        }

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