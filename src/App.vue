<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TextTag :info="arrayText"/>
  </div>
</template>

<script>
import TextTag from './components/TextTag.vue';

export default {
  name: 'App',
  components: {
    TextTag
  },
  data: () => ({
    arrayText: [{text: 'info', icon: 'mdi-home-small'}, {text: 'info'}],
  }),
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
