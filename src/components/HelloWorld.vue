<template>
  <div class="slider">
      <transition name="fade">
        <div :key="currentImageIndex">
          <img :src="currentImageSrc" alt="Slider Image">
        </div>
      </transition>
      <div class="controls">
        <button @click="previousImage">Previous</button>
        <button @click="nextImage">Next</button>
      </div>
    </div>
</template>

<script>
export default {
data() {
  return {
    images: [
      'https://placehold.co/600x400',
      'https://placehold.co/600x400',
      'https://placehold.co/600x400'
    ],
    currentImageIndex: 0,
    intervalId: null,
    autoplayDelay: 4000 // delay in milliseconds
  }
},
computed: {
  currentImageSrc() {
    return this.images[this.currentImageIndex]
  }
},
mounted() {
  this.startAutoplay()
},
methods: {
  startAutoplay() {
    this.intervalId = setInterval(() => {
      this.nextImage()
    }, this.autoplayDelay)
  },
  stopAutoplay() {
    clearInterval(this.intervalId)
  },
  previousImage() {
    this.stopAutoplay()
    this.currentImageIndex = (this.currentImageIndex - 1 + this.images.length) % this.images.length
    this.startAutoplay()
  },
  nextImage() {
    this.stopAutoplay()
    this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length
    this.startAutoplay()
  }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style>
