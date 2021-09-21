<template>
  <div id="app">
    <home-screen v-if="flagHomeScreen" v-on:new-calc="onNewCalc"></home-screen>
    <wall-calculation v-if="flagWallCalculation" v-on:back="onBackHome"></wall-calculation>
  </div>
</template>

<script>

import HomeScreen from './components/HomeScreen.vue';
import WallCalculation from './components/WallCalculation.vue';

export default {
  name: 'App',
  components: {
    HomeScreen, WallCalculation
  },
  data() {
    return {
      flagHomeScreen: true,
      flagWallCalculation: false,
    }
  },
  methods: {
    onBackHome() {
      this.flagHomeScreen = true;
      this.flagWallCalculation = false;
    },
    onNewCalc() {
      this.flagHomeScreen = false;
      this.flagWallCalculation = true;
    }
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/icon?family=Material+Icons');
@import url('https://fonts.googleapis.com/css2?family=Alegreya+Sans:wght@300;500&display=swap');
@import url('../node_modules/materialize-css/dist/css/materialize.css');
#app {
  font-family: 'Alegreya Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
