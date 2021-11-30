<template>
  <image-zoom
    :zoom="require('@/assets/mosaic.png')"
    :regular="require('@/assets/thumb.jpg')"
    :zoom-amount="7"
    click-zoom
    img-class="mosaic"
  ></image-zoom>
</template>

<script>
import imageZoom from "vue-image-zoomer";

export default {
  components: {
    imageZoom
  },
  mounted() {
    const img = new Image();
    img.onload = () => {
      console.log("img loaded");
    };
    img.src = require("@/assets/mosaic.png");
  }
};
</script>

<style>
.mosaic {
  height: 100vh;
}
</style>