<template>
    <div class="carousel">
      <PlumCarousel
        v-slot="{ currentSlide }"
        :display-counter="displayCounter"
        :total-slides="maxImages"
        class="carousel__component"
      >
        <PlumSlide
          v-for="(imgUrl, index) in imageUrls"
          :key="index"
          class="carousel__slide"
        >
          <PlumImage
            v-show="currentSlide === index + 1"
            class="carousel__image"
            :src="imgUrl"
            :alt="imgUrl"
            :lazyload="lazyload"
          />
        </PlumSlide>
      </PlumCarousel>
    </div>
</template>

<script>
import Vue from 'vue';
import VueObserveVisibility from 'vue-observe-visibility'

import PlumCarousel from '../plum-carousel/plum-carousel.vue'
import PlumImage from '../plum-image/plum-image.vue'
import PlumSlide from '../plum-slide/plum-slide.vue'

Vue.use(VueObserveVisibility);

export default {
  name: 'PlumCarouselSmart',
  components: {
    PlumCarousel,
    PlumImage,
    PlumSlide,
  },
  props: {
      imageUrls:  {
        type: Array,
        required: true,
      },
      maxImages: {
        type: Number,
        default: 30,
      },
      displayCounter: {
        type: Boolean,
        default: true,
      },
      lazyload: {
        type: Boolean,
        default: false,
      }
  },
}
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.carousel {
  // Settings: Add height and weight
  // Specific sizes can be add to support on multiple devices based on the Figma/Sketch Design
  box-sizing: border-box;
  width: 100%;
  height: 80vh;

  &__component {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__slide {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__image {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
    padding: 0 20px;
    object-fit: contain;
  }
}
</style>
