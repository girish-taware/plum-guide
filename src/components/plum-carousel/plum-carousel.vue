<template>
  <div class="plum-carousel">
    <!-- Slots: to display slides/images -->
    <div>
      <slot :current-slide="currentSlide" />
    </div>

    <!-- Navigation -->
    <div class="plum-carousel__navigation">
      <!-- Navigation Left -->
      <div
        class="plum-carousel__toggle plum-carousel__left"
        @click="previousSlide()"
        @keypress="previousSlide()"
      >
        <PlumIcon name="arrow" size="l" tabindex="0" />
      </div>
      <!-- Navigation Right with Counter -->
      <div
        class="plum-carousel__toggle plum-carousel__right"
        @click="nextSlide()"
        @keypress="nextSlide()"
      >
        <div v-if="showCounter" class="plum-carousel__count">
          <span>{{ count }}</span>
        </div>
        <PlumIcon name="arrow" size="l" :rotation="180" tabindex="0" />
      </div>
    </div>
  </div>
</template>

<script>
import PlumIcon from '../plum-icon/plum-icon.vue'

export default {
  name: 'PlumCarousel',
  components: {
    PlumIcon,
  },
  props: {
    displayCounter: {
      type: Boolean,
      default: true,
    },
    totalSlides: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      currentSlide: 1,
    }
  },
  computed: {
    count() {
      return `${this.currentSlide}/${this.totalSlides}`
    },
    showCounter() {
      return this.displayCounter && this.totalSlides > 0
    },
  },
  methods: {
    nextSlide() {
      if (this.currentSlide === this.totalSlides) {
        this.currentSlide = 1
        return
      }
      this.currentSlide += 1
    },
    previousSlide() {
      if (this.currentSlide === 1) {
        this.currentSlide = 1
        return
      }
      this.currentSlide -= 1
    },
  },
}
</script>

<style lang="scss">
.plum-carousel {
  position: relative;
  width: 100%;
  height: 100%;

  &__navigation {
    width: 100%;
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__toggle {
    display: flex;
    flex: 1;
    cursor: pointer;
  }

  &__count {
    background-color: #fff;
    width: 18px;
    height: 18px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 8px;
  }

  &__right {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 16px;
  }
}
</style>
