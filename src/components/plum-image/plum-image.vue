<template>
  <img
    v-if="lazyload"
    v-observe-visibility="loadImage"
    class="plum-image"
    :data-src="src"
    :src="blankImage"
    :alt="alt"
    @error="emitError()"
  />
  <img
    v-else
    class="plum-image plum-else"
    :src="src"
    :alt="alt"
    @error="emitError()"
  />
</template>

<script lang="ts">

export default {
  name: 'PlumImage',
  props: {
    src: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      default: '',
    },
    lazyload: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      blankImage:
        'data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==',
    }
  },
  methods: {
    loadImage(isVisible) {
      if (isVisible) {
        const dataSrcURL = this.$el.getAttribute('data-src');
        const srcURL = this.$el.getAttribute('src');

        if (dataSrcURL !== srcURL) {
          this.$el.setAttribute('src', dataSrcURL)
        }
      }
    },
    emitError() {
      this.$emit('error')
    },
  },
}
</script>

<style lang="scss">
.plum-image {
  height: auto;
  max-width: 100%;
}
</style>
