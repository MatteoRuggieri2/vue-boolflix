<template>
    <main>
        <div class="wrapper">
            
            <!-- Singolo Film -->
            <ul v-for="(movie, index) in apiObjects" :key="index">
                <li>{{ movie.title }}</li>
                <li>{{ movie.original_title }}</li>
                <li>{{ movie.original_language }}</li>
                <li>{{ movie.vote_average }}</li>
            </ul>

        </div>
    </main>
</template>

<script>
export default {
    name: 'Main',
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

        ul {
            border: 3px solid darkcyan;
            
            li {
                color: white;
            }
        }
    }
</style>