<template lang="html">
  <div class="image">
    <img :src="image.download_url">
  </div>
</template>

<script>
export default {
  name: 'image-item',
  props: ['image']
}
</script>

<style lang="css" scoped>

  .image {
    width: 100%;
    margin-bottom: 1em;
    transition: 0.2s;
    transform-origin: top center;
  }

  .image:hover {
    transform: scale(1.5);
    z-index: 1;
  }

  .image img {
    width: 100%;
    vertical-align: middle;
  }

</style>
