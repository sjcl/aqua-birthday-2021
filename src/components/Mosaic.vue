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
    <div class="buttons">
      <v-btn
        @click="showOriginal = !showOriginal"
        color="pink lighten-1"
        class="mx-2 white--text"
        large
      >Switch<br>切り替え</v-btn>
      <v-btn
        @click="showMessages = true"
        color="pink lighten-1"
        class="mx-1 white--text"
        large
      >Message/arts<br>メッセージ/アート</v-btn>
    </div>

    <v-overlay :value="showMessages" class="text-center">
      <Messages />
      <v-btn
        @click="showMessages = false"
        color="pink lighten-1"
        class="ma-2 white--text"
        large
      >Close</v-btn>
    </v-overlay>
  </div>
</template>

<script>
import imageZoom from "vue-image-zoomer";
import Messages from "@/components/Messages";

export default {
  components: {
    imageZoom,
    Messages
  },
  data() {
    return {
      loading: true,
      showOriginal: true,
      showMessages: false
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

.buttons {
  position: fixed;
  top: calc(100vh - 70px);
  left: max(100vw - 370px, 1px);
  /* right: 20px;
  bottom: 20px; */
}
</style>