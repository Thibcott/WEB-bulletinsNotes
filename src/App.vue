<template>
  <div id="app">
    <h2>bulletin de note</h2>
    <br>
    <hr>
    <br>
    <Add/>
    <br>
    <hr>
    <Epreuves/>
    
  </div>
</template>
<script>
import Epreuves from './components/Epreuves.vue'
import Add from './components/Add.vue'

export default {
  name: 'app',
  components: {
    Epreuves,
    Add
  }
}
</script>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
