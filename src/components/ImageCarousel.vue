<template>
    <ul class="gallery__list">
        <li v-for="image in imagesList" :key="image.id" class="gallery__item" @click="setImageUrl(image.download_url)">
            <img class="gallery__image" :src="image.download_url" alt="">
        </li>
    </ul>
</template>

<script>
export default {
    emits: ['getUrl'],
    name: 'ImageCarousel',
    props: {
        imagesList: Array,
    },
    methods: {
        setImageUrl(url) {
            this.$emit('getUrl', url)
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

.gallery__image {
    width: 100%;

}
</style>