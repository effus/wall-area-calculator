<template>
  <div id="app">
    <home-screen v-if="flagHomeScreen" v-on:new-calc="onNewCalc" v-on:wp-calc="onWPCalc"></home-screen>
    <wall-calculation v-if="flagWallCalculation" v-on:back="onBackHome"></wall-calculation>
    <wallpaper-calculation v-if="flagWallpaperCalc" v-on:back="onBackHome"></wallpaper-calculation>
  </div>
</template>

<script>

import HomeScreen from './components/HomeScreen.vue';
import WallCalculation from './components/WallCalculation.vue';
import WallpaperCalculation from './components/WallpaperCalculation.vue';

export default {
  name: 'App',
  components: {
    HomeScreen, WallCalculation,
    WallpaperCalculation
  },
  data() {
    return {
      flagHomeScreen: true,
      flagWallCalculation: false,
      flagWallpaperCalc: false
    }
  },
  methods: {
    onBackHome() {
      this.flagHomeScreen = true;
      this.flagWallCalculation = false;
      this.flagWallpaperCalc = false;    
    },
    onNewCalc() {
      this.flagHomeScreen = false;
      this.flagWallCalculation = true;
      this.flagWallpaperCalc = false;
    },
    onWPCalc() {
      this.flagHomeScreen = false;
      this.flagWallCalculation = false;
      this.flagWallpaperCalc = true;
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
