<template>
  <div id="app">
    <pageHeader />
    <img alt="Vue logo" src="./assets/logo.png" />
    <home />
  </div>
</template>

<script>
import pageHeader from "./components/header";
import home from "./components/home.vue";

export default {
  name: "App",
  components: {
    pageHeader,
    home
  }
};
</script>

<style>
body{
   margin: 0px;
  padding: 0px;
}
#app {
 
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
