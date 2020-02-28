<template lang="html">
  <div class="image-detail" v-if="image">
    <h3><b>{{image.author}}</b></h3>
    <p>{{image.height}} x {{image.width}}</p>
    <button type="button">View on Unsplash</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'image-detail',
  props: ['image'],
}
</script>

<style lang="css" scoped>
</style>
