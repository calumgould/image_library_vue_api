<template>
  <div id="app">
    <div class="banner">
      <h1>pic.</h1>
    </div>
    <image-grid :images="images"/>
  </div>
</template>

<script>
import ImageGrid from './components/ImageGrid.vue'

export default {
  data(){
    return {
      images: []
    }
  },
  components: {
    'image-grid': ImageGrid
  },
  mounted(){
    fetch('https://picsum.photos/v2/list')
    .then(response => response.json())
    .then(data => this.images = data)
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  width: 100%;
}

h1 {
  font-size: 5rem;
  padding: 1em 0em;
  color: white;
}

.banner {
  background: rgb(247,255,0);
  background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
  top: 0;
  left: 0;
}


</style>
