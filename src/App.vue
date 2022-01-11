<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>

import axios from 'axios';
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data: function() {
    return {
      userSearchText: '',
    }
  },
  methods: {
    
  }
};
</script>

<style lang="scss">
@import './style/general.scss';

</style>
