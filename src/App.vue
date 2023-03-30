<template>
  <div class="container">
    <the-header></the-header>
    <div v-if="images.length" class="gallery">
      <div class="gallery__enlarged--box">
        <img :src="enlargedImgUrl" alt="" class="gallery__enlarged">
      </div>
      <div class="gallery__box">
        <button class="gallery__button" @click="decrementPage">Prev
        </button>
        <image-carousel :imagesList="images" @get-url="setImageUrl"></image-carousel>
        <button class="gallery__button" @click="incrementPage">Next
        </button>
      </div>
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
      enlargedImgUrl: '',
    }
  },
  methods: {
    incrementPage() {
      this.page++;
      this.fetchImages(false);
    },
    decrementPage() {
      this.page--;
      this.fetchImages(false);
    },
    fetchImages(isFirstRender) {
      fetch(`https://picsum.photos/v2/list?page=${this.page}&limit=4`).then(res => res.json())
        .then(data => {
          this.images = data;
          if (isFirstRender) {
            this.enlargedImgUrl = this.images[0]['download_url'];
          }
        }
        )
        .catch(error => console.log(error));
    },
    setImageUrl(url) {
      this.enlargedImgUrl = url;
    }
  },
  mounted() {
    this.fetchImages(true);
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
  min-height: 900px;

}



.gallery__box {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
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

.gallery__enlarged--box {
  width: 800px;
  min-height: 550px;
  margin-left: auto;
  margin-right: auto;
}

.gallery__enlarged {
  width: 100%;
  margin-bottom: 30px;
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
