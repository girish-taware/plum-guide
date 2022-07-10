<template>
  <div class="plum-slide">
    <transition name="slide-fade">
      <slot />
    </transition>
  </div>
</template>

<script>
export default {
  name: 'PlumSlide',
}
</script>

<style lang="scss">
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: opacity 0.7s ease-in-out;
}

.slide-fade-enter {
  opacity: 0;
}

.slide-fade-leave {
  opacity: 0;
}
</style>
