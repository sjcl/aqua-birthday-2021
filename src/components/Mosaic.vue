<template>
  <p v-if="loading">Now Loading...</p>
  <div v-else>
    <img src="/original.jpg" :class="showOriginal ? 'image trans show' : 'image trans hide'" />
    <image-zoom
      zoom="/mosaic.png"
      regular="/thumb.jpg"
      :zoom-amount="7"
      click-zoom
      img-class="image"
      :class="showOriginal ? 'trans hide' : 'trans show'"
    ></image-zoom>
    <v-btn
      @click="showOriginal = !showOriginal"
      color="pink lighten-1"
      class="white--text"
      fixed
      right
      bottom
      x-large
    >Switch / 切り替え</v-btn>
  </div>
</template>

<script>
import imageZoom from "vue-image-zoomer";

export default {
  components: {
    imageZoom
  },
  data() {
    return {
      loading: true,
      showOriginal: true
    };
  },
  mounted() {
    window.onload = () => {
      this.loading = false;
      setTimeout(() => {
        this.showOriginal = false;
      }, 2000);
    };
  }
};
</script>

<style>
.image {
  height: 100vh;
}

.trans {
  display: block;
  position: absolute;
}

.show {
  opacity: 1;
  transition: opacity 2s;
}

.hide {
  opacity: 0;
  transition: opacity 2s;
}
</style>