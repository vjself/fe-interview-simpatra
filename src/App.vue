<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
export default {
  name: "app",
  components: {
    Home
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:300,600,700,800&display=swap");
#app {
  font-family: "Montserrat", sans-serif;
  -webkit-font-smoothing: antialiased;
  margin: 0 auto;
  justify-content: center;
  max-width: 1920px;
  height: 5040px;
  overflow-x: hidden;
}
</style>
