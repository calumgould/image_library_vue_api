<template lang="html">
  <div v-if="image" class="image-detail">
    <h3>by <b>{{image.author}}</b></h3>
    <p>{{image.height}} x {{image.width}}</p>
    <button type="button" @click="handleButtonClick"><b>View on Unsplash</b></button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: 'image-detail',
  props: ['image'],
  methods: {
    handleButtonClick(event){
      window.open(this.image.url)
    }
  }
}
</script>

<style lang="css" scoped>



</style>
