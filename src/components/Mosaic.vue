<template>
  <p v-if="loading">
    Now Loading...
  </p>
  <div v-else>
    <img src="/original.jpg" :class="original ? 'image trans show' : 'image trans hide'" />
    <image-zoom
      zoom="/mosaic.png"
      regular="/thumb.jpg"
      :zoom-amount="7"
      click-zoom
      img-class="image"
      :class="original ? 'trans hide' : 'trans show'"
    ></image-zoom>
    <v-btn
      @click="original = !original"
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
      original: true
    };
  },
  mounted() {
    const img = new Image();
    img.onload = () => {
      this.loading = false;
      setTimeout(() => {
        this.original = false;
      }, 2000);
    };
    img.src = "/mosaic.png";
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