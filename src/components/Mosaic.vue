<template>
<v-container><zoombox :src="require('@/assets/mosaic.png')" :thumb="require('@/assets/thumb.jpg')"></zoombox></v-container>

</template>

<script>
    export default {
        components: {
            "zoombox": require("vue-zoombox")
        }
    };
</script>