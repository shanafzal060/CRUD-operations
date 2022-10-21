<template>
  <div id="app">
    <tableApi />
  </div>
</template>

<script>
import tableApi from './components/tableApi.vue'

export default {
  name: 'App',
  components: {
    tableApi
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
