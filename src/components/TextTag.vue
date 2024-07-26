<template>
  <v-row :class="['tag', positionClass(align)]" v-resize="onResize" :style="{maxWidth: `${maxWidth}px`}">
    <div :class="['tag__cell']" v-for="({text, icon}, index) of list" :key="text + index">
      <v-chip class="tag__chip" variant="text">
        <v-icon v-if="icon">{{ icon }}</v-icon>
        {{ text }}
      </v-chip>
      <v-icon class="tag__icon" v-show="index <= lastIndex">mdi-circle-small</v-icon>
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
      list: this.info,
      lastIndex: this.info?.length,
      maxWidth: 0,
    };
  },
  mounted() {
    this.width = this.$el.offsetWidth;
    this.height = this.$el.offsetHeight;
    let lastIndex = 0;
    let width = 0;

    Array.from(this.$el.children).forEach((element, index) => {
      width += element.getBoundingClientRect().width;
      console.log(width, index);
      if (width <= this.width) {
        console.log("p");
        lastIndex = index;
      }
    });
      this.lastIndex = lastIndex;
      this.maxWidth = width;
  },
  methods: {
    onResize() {
      // this.width = width;
      // this.height = height;
      let listWidth = this.$el?.getBoundingClientRect().width;

      if (this.maxWidth < listWidth) return;

      let lastIndex = this.lastIndex;
      let width = 0;

      Array.from(this.$el.children).forEach((element, index) => {
        width += element.getBoundingClientRect().width;
        console.log(width, index);
        if (width <= listWidth) {
          console.log("p");
          lastIndex = index;
        }
      });
      this.lastIndex = lastIndex;
      this.maxWidth = width;
      console.log(lastIndex);
      console.log(this.$el?.getBoundingClientRect());
      console.dir(this.$el);
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

  },
};
</script>

<style lang="scss" scoped>
  .tag {
    display: inline-block;
    max-width: 100%;
    overflow: hidden;
    white-space: nowrap;
    &.end {
      justify-content: flex-end;
    }

    &__chip {
      background: transparent !important;
    }
    &__cell {
      display: inline-flex;
      justify-content: space-between;
      opacity: 1;
      visibility: visible;;
      &.opacity {
        opacity: 0;
        visibility: hidden;
      }
    }
    &__icon {
      margin: 0 auto;
      flex: 1;
    }
  }
</style>
