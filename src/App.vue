<template>
  <div id="app">

    <div class="banner">
      <div class="sneaky-boi"></div>
      <div class="sneaky-reveal"></div>
      <!-- <div :class="{sealHidden: scrollPosition < 150, sealVisible: scrollPosition > 150}"></div> -->
      <div class="seal" :style="{'opacity': this.opacity}"></div>
        <div class="header">
          <img src="/images/logo.png" alt="spend logo">
        </div>
    </div>
    <div class="generate-images">
      <button type="submit" @click="handlePageChange">Generate New Images</button>
    </div>
    <div class="image-grid">
      <div class="detail-border">
        <image-detail v-show="selectedImage !== null" :image="selectedImage"/>
      </div>
      <image-grid :images="images" />
    </div>
    <div class="footer">
      <div class="dreamteam">
        <svg width="260" height="45">
          <text x="0" y="40" fill="none" stroke="black" stroke-width="1" font-size="50">dreamteam
          </text>
        </svg>
      </div>
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
      selectedImage: null,
      scrollPosition: null,
      opacity: 0,
      page: 2,
      limit: 50
    }
  },
  components: {
    'image-grid': ImageGrid,
    'image-detail': ImageDetail,
  },
  mounted(){
    fetch(`https://picsum.photos/v2/list?page=${this.page}&limit=${this.amount}`)
    .then(response => response.json())
    .then(data => this.images = data)

    eventBus.$on('image-selected', (image) => {
      this.selectedImage = image
    })

    window.addEventListener('scroll', this.updateScroll)
  },
  methods: {
    updateOpacity() {
      this.opacity = this.scrollPosition/1000
    },
    updateScroll() {
      this.scrollPosition = window.scrollY
      this.updateOpacity()
    },
    handlePageChange() {
      this.page += 1
      location.reload();
      return false
    }

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
    font-family: 'Nunito'
  }

  .header {
    padding: 5% 0em;
  }


  .header img {
    max-width: 25%;
    z-index: 5;
  }

  /* .header h1:hover::after{
    content: attr(data-hover);
    font-family: 'Nunito';
    font-size: 6rem;
    padding: 1em 0em;
    color: white;
    text-align: center;
  } */


  .banner {
    background: rgb(247,255,0);
    background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
    top: 0;
    left: 0;
    width: 100%;
    height: 16.7%;
    position: relative;
    z-index: 1;
  }

  .sneaky-boi {
    height: 20px;
    width: 20px;
    position: absolute;
    top: 0;
    left: 0;
  }

  .sneaky-boi:hover {
    cursor: url('/images/seal-cursor.png'), auto;
  }

  .sneaky-boi:hover ~ .sneaky-reveal {
    opacity: 0.10;
  }

  .seal, .sealHidden, .sealVisible, .sneaky-reveal {
    position: absolute;
    z-index: -1;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: url(/images/awkwardseal.gif) center center;
    background-repeat: no-repeat;
    background-size: cover;
    opacity: 0;
    width: 100%;
    height: 100%;
  }

  .sealVisible {
    opacity: 0.15;
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

  .image-detail button, .generate-images button {
    padding: 1em 2em;
    margin-top: 0.5em;
    border-radius: 2em;
    font-size: 0.8em;
    outline: none;
    border: 1px solid black;
    font-size: 1rem;
  }

  .image-detail button:hover, .generate-images button:hover, .submit:hover {
    background: rgb(247,255,0);
    background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 80%);
    border: 1px solid white;
    color: white;
    cursor: pointer;
  }

  .generate-images button {
    margin: 2em 1em 0 1em;
    display: inline-block;
  }

  .detail-border {
    background: rgb(247,255,0);
    background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
    margin: 2em 30% 2em 30%;
    z-index: -1;
    border-radius: 2em;
    padding: 0.2em;
    position: sticky;
    top: 2%;
    z-index: 1;
  }

  .footer {
    background: rgb(247,255,0);
    background: linear-gradient(90deg, rgba(247,255,0,1) 0%, rgba(219,54,164,1) 100%);
    bottom: 0;
    left: 0;
    width: 100%;
  }

  .footer img {

  }

  .dreamteam {
    margin: 0 30%;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 3em 0 2em 0;
    display: inline-block;
  }

  text {
    font-family: 'Nunito', sans-serif;
    stroke-dasharray: 100%;
    stroke-dashoffset: 100%;

    animation: draw 8s ease 0s infinite forwards;
  }
  @keyframes draw {
    100% {
      stroke-dashoffset: 0;
    }
  }


</style>
