<template>
  <div id="app">
    <h1>Agenda webapp</h1>
    <Agenda msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Agenda from './components/Agenda.vue'

export default {
  name: 'app',
  components: {
    Agenda
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background-color: #2c3e50;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  padding-top: 60px;
  width: 100vw;
  margin-bottom: 100px;
}
</style>
