<template>
  <div id="app">
    <ChargifyForm />
  </div>
</template>

<script>
import ChargifyForm from './components/ChargifyForm.vue'

export default {
  name: 'App',
  components: {
    ChargifyForm
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
  margin-top: 40px;
}
</style>
