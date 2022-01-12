<template>
    <header>

        <div>
            <i class="fas fa-star"></i>
            LOGO
            <i class="fas fa-star"></i>
        </div>

        <div class="input-container">
            <input @keyup.enter="$emit('getUserText', userText)" v-model="userText" type="text" placeholder="Cerca un film">
            <button @click="$emit('getUserText', userText)">Cerca</button>
        </div>

    </header>
</template>

<script>
export default {
    name: 'Header',
    data: function() {
        return {
            userText: '',
        }
    }
}
</script>

<style lang='scss' scoped>

    header {
        height: 60px;
        background-color: black;
        color: white;
        display: flex;
        justify-content: space-around;
        align-items: center;

        .input-container {

            input[type=text] {
                margin-right: 5px;
            }

            button {
                cursor: pointer;
            }
        }
    }
</style>