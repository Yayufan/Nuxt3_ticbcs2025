<template>
    <div class="common-section">
        <h1 class="title">感謝下列廠商熱情贊助!!</h1>
        <!-- <img src="../assets/img/sponsor_list.png" alt=""> -->
        <div v-for="(group, groupIndex) in groupedImages" :key="groupIndex" class="image-group">
            <span v-for="(image, imgIndex) in group" :key="imgIndex" class="image-item">
                <img :src="image" alt="Sponsor Image" />
            </span>
        </div>




    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';

const modules = import.meta.glob('../assets/img/ticbcs_sponsor_logo/*.{png,jpg,jpeg,svg}', { eager: true, as: 'url' });

const sponsorImages = ref<string[]>(Object.values(modules));

const groupedImages = ref<string[][]>([]);

watch(sponsorImages, (newValue) => {
    sponsorImages.value.forEach((image, index) => {
    const groupIndex = Math.floor(index / 3);
    if (!groupedImages.value[groupIndex]) {
        groupedImages.value[groupIndex] = [];
    }
    groupedImages.value[groupIndex].push(image);
});
}, { immediate: true });




</script>
<style lang="scss" scoped>
.common-section {
    margin: $common-section-margin;
    width: $common-section-width;
    font-family: $common-section-font-family;
    justify-content: center;
    align-items: center;
    display: flex;
    flex-direction: column;
    gap: 2.5rem;

    .title {
        font-size: 2rem;
        font-weight: 700;
        margin: 0rem 0 1rem 0;
    }
    .image-group {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 2rem;
       .image-item {
        width:30%;
        img {
            width: 100%;
            height: auto;
            max-width: 100%;
            max-height: 100%;
            object-fit: cover;
        }
       }
    }
}
</style>