<template>
    <div class="common-section">
        <img src="../assets/img/mascat_info.png" alt="">
    </div>
</template>
<script lang="ts" setup></script>
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

    img {
        width: 100%;
        height: auto;
        max-width: 800px; // Adjust the max-width as needed
        border-radius: 10px; // Optional: add some border radius for aesthetics
    }
}
</style>