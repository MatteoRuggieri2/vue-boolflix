<template>
    <header>

        <div>
            LOGO
        </div>

        <div class="input-container">
            <input type="text" placeholder="Cerca un film">
            <button>Cerca</button>
        </div>

    </header>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style lang='scss' scoped>

    header {
        background-color: black;
        color: white;
        display: flex;
        justify-content: space-around;
        padding: 20px 0;

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