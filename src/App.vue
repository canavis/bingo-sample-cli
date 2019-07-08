<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <SetNumber/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SetNumber from './components/SetNumber.vue'
// import NumberList from './components/NumberList.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    SetNumber,
    // NumberList
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
