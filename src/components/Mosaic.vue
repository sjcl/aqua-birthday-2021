<template>
<div>
  <img :src="require('@/assets/sample.jpg')" :class="original ? 'image trans show' : 'image trans hide'" />
  <image-zoom
    :zoom="require('@/assets/mosaic.png')"
    :regular="require('@/assets/thumb.jpg')"
    :zoom-amount="7"
    click-zoom
    img-class="image"
    :class="original ? 'trans hide' : 'trans show'"
  ></image-zoom>
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
      original: true
    };
  },
  mounted() {
    const img = new Image();
    img.onload = () => {
      console.log("img loaded");
    };
    img.src = require("@/assets/mosaic.png");

    setInterval(() => {
      this.original = false
    }, 1000)
  }
};
</script>

<style>
div {
	font-size: 0;
	line-height: 0;
}

.image {
  height: 100vh;
}

.trans {
  position: absolute;
}

.show {
  opacity: 1;
  transition: opacity 1.5s;
}

.hide {
  opacity: 0;
  transition: opacity 1.5s;
}
</style>