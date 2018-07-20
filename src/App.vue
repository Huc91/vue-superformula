<template>
  <div id="app">
    <SuperFormula/>
  </div>
</template>

<script>
import SuperFormula from './components/SuperFormula.vue'

export default {
  name: 'app',
  components: {
    SuperFormula
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
