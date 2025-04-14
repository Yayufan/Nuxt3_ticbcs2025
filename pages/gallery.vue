<template>
    <div class="common-section">
        <h1 class="title">感謝下列廠商熱情贊助!!</h1>
        <!-- <img src="../assets/img/sponsor_list.png" alt=""> -->

        <div class="gallery">
            <div v-for="(group, groupIndex) in groupedImages1" :key="groupIndex" class="image-group">
                <span v-for="(image, imgIndex) in group" :key="imgIndex" class="image-item">
                    <img :src="image" alt="Sponsor Image" />
                </span>
            </div>
        </div>

        <div class="gallery">
            <div v-for="(group, groupIndex) in groupedImages2" :key="groupIndex" class="image-group">
                <span v-for="(image, imgIndex) in group" :key="imgIndex" class="image-item">
                    <img :src="image" alt="Sponsor Image" />
                </span>
            </div>
        </div>




    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';

const modules1 = import.meta.glob('../assets/img/ticbcs_gallery/*.{png,jpg,jpeg,svg}', { eager: true, as: 'url' });

const galleryImages1 = ref<string[]>(Object.values(modules1));

const groupedImages1 = ref<string[][]>([]);

watch(galleryImages1, (newValue) => {
    galleryImages1.value.forEach((image, index) => {
        const groupIndex = Math.floor(index / 6);
        if (!groupedImages1.value[groupIndex]) {
            groupedImages1.value[groupIndex] = [];
        }
        groupedImages1.value[groupIndex].push(image);
    });
}, { immediate: true });

const modules2 = import.meta.glob('../assets/img/ticbcs_gallery2/*.{png,jpg,jpeg,svg}', { eager: true, as: 'url' });

const galleryImages2 = ref<string[]>(Object.values(modules2));

const groupedImages2 = ref<string[][]>([]);

watch(galleryImages2, (newValue) => {
    galleryImages2.value.forEach((image, index) => {
        const groupIndex = Math.floor(index / 6);
        if (!groupedImages2.value[groupIndex]) {
            groupedImages2.value[groupIndex] = [];
        }
        groupedImages2.value[groupIndex].push(image);
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

    .gallery {
        border-width: 0px 0 1px 0;
        border-style: solid;
        border-color: #D3D3D3;


        .image-group {
            display: flex;
            justify-content: flex-start;
            align-items: center;
            gap: 2rem;
            margin-bottom: 1rem;
            width: 100%;

            .image-item {
                width: calc(100% / 6 - 2rem);

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

}
</style>