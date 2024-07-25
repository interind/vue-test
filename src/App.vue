<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <div class="content" v-for="item in [100, 80, 60, 40]" :key="item" :style="`width: ${item}%`">
      <TextTag :info="arrayText"/>
    </div>
  </div>
</template>

<script>
import TextTag from './components/TextTag.vue';
import data from './data/text.json';

export default {
  name: 'App',
  components: {
    TextTag
  },
  data: () => ({
    arrayText: data,
  }),
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.content {
  display: block;
  padding: 20px;
}
</style>
