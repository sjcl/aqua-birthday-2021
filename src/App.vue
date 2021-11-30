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

<style scoped>
body {
  scrollbar-width: none;
}

body::-webkit-scrollbar {
  display: none;
}

#app {
  background: url('/background.png');
  background-size: cover;
}
</style>