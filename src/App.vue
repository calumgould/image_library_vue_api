<template>
  <div id="app">

    <div class="banner">
      <div class="header">
        <h1 data-hover="Spend.">pic.</h1>
      </div>
    </div>
    <div class="image-grid">
      <div class="detail-border">
        <image-detail v-show="selectedImage !== null" :image="selectedImage"/>
      </div>
      <image-grid :images="images" />
    </div>
    <div class="footer">
      <img src="/images/Unsplash_Symbol.png" alt="Unsplash logo">
    </div>
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
  text-align: center;
}

h1 {
  font-size: 6rem;
  color: white;
  text-align: center;
  margin: 0 30%;
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

.image-detail {
  padding: 2em 1em;
  border-radius: 2em;
  background-color: white;
}

.image-detail p {
  color: black;
  padding-bottom: 0.5em;
}

.image-detail button {
  padding: 1em 2em;
  margin-top: 0.5em;
  border-radius: 2em;
  font-size: 0.8em;
  outline: none;
  border: 1px solid black;

}

.image-detail button:hover {
  background: rgb(247,255,0);
  background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 80%);
  border: 1px solid white;
  color: white;
  cursor: pointer;
}



.detail-border {
  background: rgb(247,255,0);
  background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
  margin: 2em 30% 2em 30%;
  z-index: -1;
  border-radius: 2em;
  padding: 0.2em;
}

.footer {
  background: rgb(247,255,0);
  background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
  bottom: 0;
  left: 0;
  width: 100%;
}


</style>
