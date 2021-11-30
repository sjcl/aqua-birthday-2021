<template>
  <p v-if="loading">Now Loading...</p>
  <div v-else>
    <img src="/original.jpg" :class="getOriginalImageClass()" />
    <image-zoom
      zoom="/mosaic.png"
      regular="/thumb.jpg"
      :zoom-amount="7"
      click-zoom
      :img-class="getImageClass()"
      :class="showOriginal ? 'trans hide' : 'trans show'"
    ></image-zoom>
    <div class="buttons">
      <v-btn
        @click="showOriginal = !showOriginal"
        color="pink lighten-1"
        class="mx-1 white--text"
        large
      >
        Switch
        <br />切り替え
      </v-btn>
      <v-btn @click="showMessages = true" color="pink lighten-1" class="mx-1 white--text" large>
        Message/arts
        <br />メッセージ/アート
      </v-btn>
      <v-btn @click="showCredits = true" color="pink lighten-1" class="mx-1 white--text" large>
        Credits
        <br />クレジット
      </v-btn>
    </div>

    <v-overlay :value="showMessages" opacity=".6" absolute class="text-center">
      <Messages />
      <v-btn
        @click="showMessages = false"
        color="pink lighten-1"
        class="ma-2 white--text"
        large
      >Close</v-btn>
    </v-overlay>

    <v-overlay :value="showCredits" opacity=".6" absolute class="text-center">
      <Credits />
      <v-btn
        @click="showCredits = false"
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
import Credits from "@/components/Credits";

export default {
  components: {
    imageZoom,
    Messages,
    Credits
  },
  data() {
    return {
      loading: true,
      showOriginal: true,
      showMessages: false,
      showCredits: false,
      isMobile: window.screen.width < window.screen.height
    };
  },
  mounted() {
    console.log(this.isMobile);
    window.onload = () => {
      this.loading = false;
      setTimeout(() => {
        this.showOriginal = false;
      }, 2000);
    };
  },
  methods: {
    getImageClass() {
      if (this.isMobile) return "image-mobile";
      return "image";
    },
    getOriginalImageClass() {
      if (this.isMobile) {
        if (this.showOriginal) return "image-mobile trans show";
        return "image-mobile trans hide";
      } else {
        if (this.showOriginal) return "image trans show";
        return "image trans hide";
      }
    }
  }
};
</script>

<style>
.image {
  width: 100vw;
  
}

.image-mobile {
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
  left: max(100vw - 425px, 1px);
  /* right: 20px;
  bottom: 20px; */
}
</style>