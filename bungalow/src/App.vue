<template>
  <div id="app">
    <Navbar />
    <Grid />
  </div>
</template>

<script>
import Navbar from './components/Navbar'
import Grid from './components/Grid'

export default {
  name: 'app',
  components: {
    Navbar,
    Grid
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
