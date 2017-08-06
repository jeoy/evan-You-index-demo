<template>
  <div id="app">
    <img class="logo" src="./assets/logo.png">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
    name: 'app'
};
</script>

<style>
html, body {
    margin: 0;
    padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.logo {
    width: 50%;
}
</style>
