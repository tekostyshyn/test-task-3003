<template>
    <div class="gallery__urlslist">
    <h2>List of selected image urls:</h2>
    <ul>
        <li v-for="image of selectedImages" :key="image.id">
        {{ image.url  }}</li>
    </ul>
</div>
</template>

<script>
export default {
    name: 'ImageList',
    props: {
        selectedImages: Array,
    },
}
</script>