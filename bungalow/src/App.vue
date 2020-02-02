<template>
  <div id="app">
    <Card />
    <Navbar />
  </div>
</template>

<script>
import Card from './components/Card'
import Navbar from './components/Navbar'

export default {
  name: 'app',
  components: {
    Navbar,
    Card
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
