<template>
  <div id="app">
    <GamesApi>

    </GamesApi>
  </div>
</template>

<script>

import GamesApi from '../components/GamesApi.vue';

export default {
  name: 'App',
  data(){
    return{

    }
  },
  components: {
    GamesApi
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
