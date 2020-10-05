<template>
  <div id="app">
    <lista-telefonica/>
  </div>
</template>

<script>
import ListaTelefonica from './components/ListaTelefonica.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    ListaTelefonica
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
