<template>
  <div class="tag">
    <div class="tag__cell" v-for="({text, icon}, index) of info" :key="text + index">
      <v-chip class="tag__chip" variant="text">
        <v-icon v-if="icon">{{ icon }}</v-icon>
        {{ text }}
      </v-chip>
      <v-icon class="tag__icon" v-if="index < info?.length - 1">mdi-circle-small</v-icon>
    </div>
  </div>
</template>

<script>

export default {
  name: 'TextTag',
  props: {
    info: {type: [], require: false}},
  data: () => ({}),
  methods: {
    separators:  (info) => info?.slice(0, info?.length - 1) || []
  },
}
</script>

<style lang="scss" scoped>
  .tag {
    display: inline-flex;
    flex-wrap: wrap;
    width: 100%;
    &__chip {
      background: transparent !important;
    }
    &__cell {
      display: flex;
      justify-content: space-between;
      flex: 1;
    }
    &__icon {
      margin: 0 auto;
    }
  }
</style>
