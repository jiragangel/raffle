<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
  height: 100vh
}
body {
  margin: 0
}
@font-face {
  font-family: "Chalk";
  src: local("Chalk"),
   url(./fonts/KGTenThousandReasons.ttf) format("truetype");
}
h1 {
  font-size: 75px;
  margin-top: 60px !important;
}
h2 {
  font-size: 50px
}
h1, h2, h3 {
  font-family: 'Chalk'
}
</style>
