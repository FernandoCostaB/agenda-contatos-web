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
    ListaTelefonica
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 10px;
}
</style>
