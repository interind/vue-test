<template>
  <v-row v-if="info?.length" :class="['tag', positionClass(align)]" :style="{maxHeight: `${maxHeight}px`}">
    <div class="tag__cell" v-for="({text, icon}, index) of currentList" :key="text + index">
      <v-icon class="tag__icon" v-show="index">mdi-circle-small</v-icon>
      <v-chip class="tag__chip" variant="text">
        <v-icon v-if="icon">{{ icon }}</v-icon>
        {{ text }}
      </v-chip>
    </div>
  </v-row>
</template>

<script>

export default {
  name: 'TextTag',
  inheritAttrs: false,
  props: {
    info: {type: [], require: false, default: []},
    align: String,
  },
  data() {
    return {
      width: 0,
      height: 0,
      maxHeight: 0,
      currentList: [],
    };
  },
  mounted() {
    this.maxHeight = this.$el.children[0]?.offsetHeight || 0;
  },
  created() {
    this.currentList = Array.isArray(this.info) ? this.info : [];
  },
  methods: {
    positionClass(align) {
      switch(align) {
        case 'right':
        case 'end':
          return 'end';
        default:
          return 'start';
      }
    },
  },
};
</script>

<style lang="scss" scoped>
  .tag {
    display: inline-flex;
    flex-wrap: wrap;
    width: 100%;
    max-width: 100%;
    outline: 1px solid red;
    overflow-y: hidden;
    &::-webkit-scrollbar {
      display: none;
    }
    &.end {
      justify-content: flex-end;
    }

    &__chip {
      background: transparent !important;
    }
    &__cell {
      display: inline-flex;
      justify-content: space-between;
    }
    &__icon {
      flex: 1;
      margin: 0 auto;
    }
  }
</style>
