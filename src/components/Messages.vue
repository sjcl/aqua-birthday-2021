<template>
  <v-container class="overlay overflow-y-auto">
    <div class="text-center text-h4 my-1">Messages</div>
    <div class="text-center text-h4 my-1">メッセージ</div>
    <v-row>
      <v-col v-for="msg in messages" :key="msg" cols="12" lg="3" md="6"  sm="12">
        <v-img :src="'/messages/'+msg+'.jpg'" max-width="100vw" />
      </v-col>
    </v-row>
    <div class="text-center text-h4 my-1">Arts</div>
    <div class="text-center text-h4 my-1">アート</div>
    <v-row>
      <v-col v-for="img in images" :key="img" cols="12" lg="3" md="6" sm="12">
        <v-img :src="'/images/'+img+'.jpg'" max-width="100vw"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      messages: [...Array(87)].map((_, i) => "Message " + (i + 1)),
      images: [...Array(7)].map((_, i) => "Image " + (i + 2)),
    };
  }
};
</script>

<style>
.overlay {
  max-height: 90vh;
}
</style>