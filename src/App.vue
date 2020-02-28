<template>
  <div id="app">
    <div class="banner">
      <div class="header">
        <h1 data-hover="Spend.">pic.</h1>
      </div>
    </div>
    <image-grid :images="images"/>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import ImageGrid from './components/ImageGrid.vue'
import ImageDetail from './components/ImageDetail.vue'

export default {
  data(){
    return {
      images: [],
      selectedImage: null
    }
  },
  components: {
    'image-grid': ImageGrid,
    'image-detail': ImageDetail
  },
  mounted(){
    fetch('https://picsum.photos/v2/list')
    .then(response => response.json())
    .then(data => this.images = data)

    eventBus.$on('image-selected', (image) => {
      this.selectedImage = image
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  width: 100%;
}

h1 {
  font-size: 6rem;
  color: white;
  text-align: center;
  margin: 0 40%;
}

.header {
  padding: 6em 0em
}

.header h1:hover {
  font-size: 0;
}

.header h1:hover::after{
  content: attr(data-hover);
  font-family: 'Nunito';
  font-size: 6rem;
  padding: 1em 0em;
  color: white;
  text-align: center;
}


.banner {
  background: rgb(247,255,0);
  background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
  top: 0;
  left: 0;
  width: 100%;
}


</style>
