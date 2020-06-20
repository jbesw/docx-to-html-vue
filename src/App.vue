<template>
  <div id="app">
    <Convert msg="DOCX to HTML converter"/>
  </div>
</template>

<script>
import Convert from './components/Convert.vue'

export default {
  name: 'App',
  components: {
    Convert
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
