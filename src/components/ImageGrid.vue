<template lang="html">
  <div class="image-grid">
    <image-item v-for="(image, index) in images" :image="image" :key="index"/>
  </div>
</template>

<script>
import Image from './Image.vue'

export default {
  name: 'image-grid',
  props: ['images'],
  components: {
    'image-item': Image
  }
}
</script>

<style lang="css" scoped>

  .image-grid {
    justify-content: center;
    column-count: 4;
    line-height: 0;
    column-gap: 1em;
    text-align: center;
    margin: 4em 10em;
  }

</style>
