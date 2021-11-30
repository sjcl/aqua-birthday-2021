<template>
  <v-container class="overlay overflow-y-auto">
    <v-row>
      <v-col v-for="msg in messages" :key="msg" cols="3">
        <v-img :src="'/messages/'+msg+'.jpg'" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      messages: [...Array(42)].map((_, i) => "Message " + (i + 1))
    };
  }
};
</script>

<style>
.overlay {
    max-height: 90vh;
}
</style>