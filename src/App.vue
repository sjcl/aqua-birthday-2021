<template>
  <v-app>
    <Mosaic />
  </v-app>
</template>

<script>
import Mosaic from "./components/Mosaic";

export default {
  name: "App",

  components: {
    Mosaic
  },

  data: () => ({
    //
  })
};
</script>

<style>
html {
overflow: hidden;
}
/* html {
  scrollbar-width: none;
}

html::-webkit-scrollbar:horizontal {
  display: none;
} */

#app {
  background: url("/background.png");
  background-size: cover;
  overflow-x: scroll;
}
</style>