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
    column-count: 3;
    line-height: 0;
    column-gap: 1em;
    text-align: center;
    margin: 2em 10%;
    padding-bottom: 10%;
  }

  @media only screen and (max-width: 1000px) {
    .image-grid {
      column-count: 2;
    }
  }

  @media only screen and (max-width: 700px) {
    .image-grid {
      column-count: 1;
    }
  }

</style>
