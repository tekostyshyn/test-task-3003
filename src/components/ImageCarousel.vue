<template>
    <ul class="gallery__list">
        <li v-for="image in imagesList" :key="image.id" class="gallery__item" 
        :class="{ 'gallery__item--choosen': checkIfSelected(image) }"
        @click="selectImage(image.download_url, image.id)">
          <img class="gallery__image" :src="image.download_url" alt="">
        </li>
    </ul>
    <div>
    </div>
</template>

<script>

export default {
    emits: ['getUrl', 'selectImage'],
    name: 'ImageCarousel',
    props: {
        imagesList: Array,
    },
    data() {
        return {
            selectedImages: [
            ]
        }
    },
    methods: {
        selectImage(url, id) {
            this.$emit('getUrl', url);
            let index =  this.selectedImages.findIndex(el => el.id === id);
            if (index >= 0) {
                this.selectedImages.splice(index, 1)
            } else (
                this.selectedImages.push({id: id, url: url})
            );
            this.$emit('selectImage', this.selectedImages)
        },
        checkIfSelected(image) {
            let index =  this.selectedImages.findIndex(el => el.id === image.id);
            return index >= 0 ? true : false;
        }
    }
}
</script>

<style scoped>
.gallery__list {
    display: flex;
    justify-content: space-between;
    gap: 20px;
    cursor: pointer;
}

.gallery__item {
    width: 270px;
    height: 180px;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
}

.gallery__item--choosen {
    border: 4px solid orange;
}

.gallery__image {
    width: 100%;

}
</style>