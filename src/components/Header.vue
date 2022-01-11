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