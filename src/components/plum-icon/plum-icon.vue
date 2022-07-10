<template>
  <div class="plum-icon" :style="getSize">
    <component
      :is="icons[name]"
      :style="{ ...getStyle, ...getSize }"
      class="plum-icon__svg"
    />
  </div>
</template>

<script lang="ts">
import arrow from './icons/arrow.vue'

const icons = {
  arrow
};
const iconsList = ['arrow'];

const sizes = {
  xs: 12,
  s: 18,
  m: 24,
  l: 30,
  xl: 42,
  xxl: 48,
  xxxl: 80,
}

export default {
  name: 'PlumIcon',
  props: {
    name: {
      type: String,
      required: true,
      validator: val => iconsList.includes(val),
    },
    size: {
      type: String,
      default: 'm',
      validator: val => val in sizes,
    },
    rotation: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      sizes,
      icons,
    }
  },
  computed: {
    getStyle() {
      const style = {
        transform: `rotate(${this.rotation}deg)`,
      }
      return style
    },
    getSize() {
      const size = `${this.sizes[this.size]}px`
      return {
        width: size,
        height: size,
        minWidth: size,
        minHeight: size,
      }
    },
  },
}
</script>

<style lang="scss">
.plum-icon {
  &__svg {
    pointer-events: none;
  }
}
</style>
