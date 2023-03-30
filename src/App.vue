<template>
  <div class="container">
    <the-header></the-header>
    <div v-if="images.length" class="gallery">
      <button class="gallery__button" @click="decrementPage">Prev
      </button>
      <image-carousel :imagesList="images"></image-carousel>
      <button class="gallery__button" @click="incrementPage">Next
      </button>
    </div>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import ImageCarousel from './components/ImageCarousel.vue';

export default {
  name: 'App',
  components: {
    TheHeader,
    ImageCarousel
  },
  data() {
    return {
      page: 1,
      imagesPerPage: 4,
      images: [],
      areButtonsShowed: true,
    }
  },
  methods: {
    incrementPage() {
      this.page++;
      this.fetchImages();
    },
    decrementPage() {
      this.page--;
      this.fetchImages();
    },
    fetchImages() {
      fetch(`https://picsum.photos/v2/list?page=${this.page}&limit=4`).then(res => res.json())
        .then(data => this.images = data)
        .catch(error => console.log(error));
    }
  },
  mounted() {
    this.fetchImages();
  }
}
</script>

<style>
li,
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.container {
  padding: 0 15px;
  width: 1280px;
  margin-left: auto;
  margin-right: auto;
}

.gallery {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  min-height: 180px;
}

.gallery__button {
  min-height: 20px;
  width: 60px;
  border: none;
  background-color: transparent;
  color: black;
  cursor: pointer;
  font-size: 18px;
  font-weight: 500;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
