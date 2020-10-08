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
}
body {
  margin: 0
}
@font-face {
  font-family: "Chalk";
  src: local("Chalk"),
   url(./fonts/KGTenThousandReasons.ttf) format("truetype");
}
h1, h2, h3 {
  font-family: 'Chalk'
}
</style>
