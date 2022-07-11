<template>
  <div id="app">
     <!-- For Demo purpose, option to toggle between 2 type of carousels -->
    <div>
      <label>Switch to:</label>
      <button id="btn-toggle" @click="toggleCarousel">{{ showSmartCarousel ? 'Smart Carousel' : 'Configurable Carousel' }}</button>
    </div>
    <!-- Carousel Type 1: Carousel with configurablle slides -->
    <div v-show="!showSmartCarousel" class="carousel">
      <PlumCarousel
        v-slot="{ currentSlide }"
        :display-counter="true"
        :total-slides="numberOfImages"
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
            :lazyload="true"
          />
        </PlumSlide>
      </PlumCarousel>
    </div>
     <!-- Carousel Type 2: Smart Image Carousel -->
    <div v-show="showSmartCarousel" class="carousel">
      <PlumCarouselSmart
        class="carousel__component carousel__smart-component"
        :image-urls="imageUrls"
        :max-images="numberOfImages"
        :lazyload="true"
        :display-counter="true"
      >
      </PlumCarouselSmart>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import VueObserveVisibility from 'vue-observe-visibility'

import PlumCarousel from './components/plum-carousel/plum-carousel.vue'
import PlumCarouselSmart from './components/plum-carousel-smart/plum-carousel-smart.vue'
import PlumImage from './components/plum-image/plum-image.vue'
import PlumSlide from './components/plum-slide/plum-slide.vue'

Vue.use(VueObserveVisibility);

export default {
  name: 'App',
  components: {
    PlumCarousel,
    PlumCarouselSmart,
    PlumImage,
    PlumSlide,
  },
  data() {
    return {
      numberOfImages: 30,
      imageUrls: [],
      imageAPI: 'https://run.mocky.io/v3/8dac4388-ce28-4406-95bb-91aec813168d', // To add in environment variables
      showSmartCarousel: true,
    }
  },
  async mounted() {
    const imageUrls = await this.getImageUrls();
    // Business Rule: Show only top 30 images
    this.imageUrls = imageUrls.slice(0, this.numberOfImages);
  },
  methods: {
    async getImageUrls() {
      try {
        const response = await fetch(this.imageAPI);
        const data = await response.json();
        return data.imageUrls
      } catch(err) {
        // Send error to Error Monitoring Tool such as SENTRY
        console.log('[Images API] ERROR', err);
      }
    },
    toggleCarousel() {
      this.showSmartCarousel = !this.showSmartCarousel;
    }
  }
}
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

#btn-toggle {
  width: 160px;
  height: 40px;
  margin-bottom: 24px;
  text-align: left;
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
