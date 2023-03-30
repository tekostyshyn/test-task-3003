<template>
    <ul class="gallery__list">
        <li v-for="image in imagesList" :key="image.id" class="gallery__item">
            <img class="gallery__image" :src="image.download_url" alt="">
        </li>
    </ul>
</template>

<script>
export default {
    name: 'ImageCarousel',
    props: {
        imagesList: Array,
    },
}
</script>

<style scoped>
.gallery__list {
    display: flex;
    justify-content: space-between;
    gap: 20px;
}
.gallery__image {
    width: 270px;
}
</style>