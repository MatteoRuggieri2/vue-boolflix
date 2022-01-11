<template>
    <main>
        <div class="wrapper">
            <ul v-for="(movie, index) in apiObjects" :key="index">
                <li>{{ apiObjects.title }}</li>
                <li>{{ apiObjects.original_title }}</li>
                <li>{{ apiObjects.original_language }}</li>
                <li>{{ apiObjects.vote_average }}</li>
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