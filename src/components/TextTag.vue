<template>
  <div class="row">
    <div v-for="({text, icon}, index) of info" :key="text + index">
      <v-chip>
        <v-icon v-if="icon">{{ icon }}</v-icon>
        {{ text }}
      </v-chip>
      <v-icon v-if="index < info?.length - 1">mdi-circle-small</v-icon>
    </div>
  </div>
</template>

<script>

export default {
  name: 'TextTag',
  props: {
    info: {type: [], require: false}},
  data: () => ({}),
}
</script>

<style lang="scss" scoped>
  .row {
    display: flex;
    justify-content: space-around;
  }
</style>
