<template>
    <header>

        <div>
            LOGO
        </div>

        <div class="input-container">
            <input v-model="userText" type="text" placeholder="Cerca un film">
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