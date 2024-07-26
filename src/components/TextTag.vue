<template>
  <v-row :class="['tag', positionClass(align)]" v-resize="onResize">
    <div class="tag__cell" v-for="({text, icon}, index) of renderList" :key="text + index">
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
      currentList: [],
      lastIndex: this.info?.length - 1,
    };
  },
  mounted() {
    this.width = this.$el.offsetWidth;
    this.height = this.$el.offsetHeight;
    this.currentList = this.info;
  },
  methods: {
    onResize() {
      // this.width = width;
      // this.height = height;
      this.lastIndex = this.info?.length;
      let lastIndex = this.lastIndex;
      let width = 0;
      const listWidth = this.$el?.getBoundingClientRect().width;

      console.log(listWidth, this.$el.children);

      Array.from(this.$el.children).forEach((element, index) => {
        width += element.getBoundingClientRect().width;
        if (width <= listWidth) {
          lastIndex = index;
        }
      });
      console.log(width);
      this.lastIndex = lastIndex + 1;
    },
    positionClass(align) {
      switch(align) {
        case 'right':
        case 'end':
          return 'end';
        default:
          return 'justify-start';
      }
    },
  },
  computed: {
    renderList() {
      return this.info.slice(0, this.lastIndex);
    }
  }
};
</script>

<style lang="scss" scoped>
  .tag {
    display: inline-flex;
    flex-wrap: nowrap;
    width: 100%;
    outline: 1px solid red;
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
