<template>
  <div id="app">

  </div>
</template>

<script>
import About from './components/About'
import Customer from './components/Customers'

export default {
  name: 'app',
  components: {
    About,
    Customer
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
