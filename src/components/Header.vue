<template>
    <header>

        <div class="header-left">
            <div class="logo">
                <img src="../assets/img/logo_netflix.png" alt="Logo Netflix">
            </div>
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
        padding: 0 20px;
        background-color: black;
        color: white;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .header-left {

            .logo {
                width: 100px;
            }
        }

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