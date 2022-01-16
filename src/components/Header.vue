<template>
    <header>

        <div class="header-left">
            <div @click="$emit('backHome', true); clearMovieSearch()" class="logo">
                <img src="../assets/img/logo_netflix.png" alt="Logo Netflix">
            </div>

            <div class="links-list">
                <ul>
                    <li @click="$emit('backHome', true); clearMovieSearch()">Home</li>
                    <li>Serie TV</li>
                    <li>Film</li>
                </ul>
            </div>
        </div>

        <div class="input-container">
            <input @keyup.enter="$emit('getUserText', userText)" v-model="userText" type="text" placeholder="CERCA UN FILM">
            <span @click="$emit('getUserText', userText)" class="lens-icon"><i class="fas fa-search"></i></span>
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
    },
    methods: {
        clearMovieSearch: function() {
            this.userText = '';
        }
    }
}
</script>

<style lang='scss' scoped>
@import '../style/variables.scss';

    header {
        height: 60px;
        padding: 0 20px;
        background-color: black;
        color: $primary_text_color;
        display: flex;
        justify-content: space-between;
        align-items: center;

        .header-left {
            display: flex;
            align-items: center;

            .logo {
                width: 100px;
                margin-right: 30px;
                cursor: pointer;
            }

            .links-list {

                ul {
                    list-style-type: none;
                    display: flex;

                    li {
                        margin: 0 10px;
                        font-family: $title_text_font;
                        font-size: 16px;
                        cursor: pointer;

                        &:hover {
                            color: rgb(209, 209, 209);
                        }
                    }
                }
            }
        }

        .input-container {
            display: flex;
            align-items: center;

            input[type=text] {
                margin-right: 10px;
                padding: 2px 10px;
                border-radius: 10px;
                border: none;
                font-family: $primary_text_font;
                font-size: 14px;
            }

            .lens-icon {
                display: inline-block;
                padding-top: 4px;
                cursor: pointer;
            }
        }
    }
</style>