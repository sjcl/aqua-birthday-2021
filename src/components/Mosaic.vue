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

    <div v-if="isMobile" class="buttons-mobile">
      <v-btn @click="showOriginal = !showOriginal" color="pink lighten-1" class="mx-1" fab>
        <v-icon color="white">mdi-sync</v-icon>
      </v-btn>
      <v-menu offset-y offset-overflow tile>
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="pink lighten-1" class="mx-1" fab>
            <v-icon color="white" v-bind="attrs" v-on="on">mdi-dots-vertical</v-icon>
          </v-btn>
        </template>
        <v-btn @click="showMessages = true" color="pink lighten-1" class="my-1 ml-auto white--text d-block" large>
          Message/arts
          <br />メッセージ/アート
        </v-btn>
        <v-btn @click="showCredits = true" color="pink lighten-1" class="my-1 ml-auto white--text d-block" large>
          Credits
          <br />クレジット
        </v-btn>
      </v-menu>
    </div>
    <div v-else class="buttons">
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
      fillHeight: window.innerWidth / 16 < window.innerHeight / 9,
      isMobile: window.innerWidth < 800
    };
  },
  mounted() {
    window.onload = () => {
      this.loading = false;
      setTimeout(() => {
        this.showOriginal = false;
      }, 2000);

      document.getElementById("app").onwheel = this.onWheel;
    };
  },
  methods: {
    getImageClass() {
      if (this.fillHeight) return "image-h";
      return "image-w";
    },
    getOriginalImageClass() {
      if (this.fillHeight) {
        if (this.showOriginal) return "image-h trans show";
        return "image-h trans hide";
      } else {
        if (this.showOriginal) return "image-w trans show";
        return "image-w trans hide";
      }
    },
    onWheel(event) {
      document.getElementById("app").scrollLeft += event.deltaY;
    }
  }
};
</script>

<style>
.image-w {
  width: 100vw;
}

.image-h {
  height: 100vh;
  width: calc(100vh * (16 / 9));
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
  /* top: calc(100vh - 70px);
  left: max(100vw - 425px, 1px); */
  right: 20px;
  bottom: 20px;
}

.buttons-mobile {
  position: fixed;
  right: 5px;
  bottom: 5px;
}

.v-menu__content {
  box-shadow: none !important;
}
</style>