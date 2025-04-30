<template>
    <header class="header">
        <!-- <div class="title" v-if="title != ''">
            <p>{{ title.split('(')[0] }}</p>
            <p>{{ title.split('y')[1] }}</p>
        </div> -->
    </header>
</template>
<script lang="ts" setup>


const router = useRouter();

const title = ref('');
watch(() => router.currentRoute.value.path, (value) => {
    switch (value) {
        case '/seminar-registration':
            title.value = '研討會報名';
            break;
        case '/credit-application':
            title.value = '學分申請';
            break;
        case '/sponsor-list':
            title.value = '贊助廠商';
            break;
        case '/mascot':
            title.value = '吉祥物專區';
            break;
        case '/gallery':
            title.value = 'Gallery (2023 TICBCS)';
            break;
        default:
            title.value = '';
            break;
    }
});

const isActive = ref(false);
const props = defineProps<{
    isActive: boolean;
}>();

watch(() => props.isActive, (value) => {
    isActive.value = value;
});

const isScroll = ref(false)

function handleScroll() {
    // 獲取滾動到的位置
    let scrollPositionY = window.scrollY
    if (scrollPositionY > 0) {
        isScroll.value = true
    } else {
        isScroll.value = false
    }
}

onMounted(() => {
    window.addEventListener('scroll', handleScroll)
})


</script>
<style lang="scss" scoped>
.header {
    display: flex;
    justify-content: center;
    align-items: center;
    // background: url('../../assets/img/ticbcsBanner_new (1).jpg') no-repeat center center;
    background: url('../../assets/img/ticbcsBanner_new.jpg') no-repeat bottom center;
    background-size: cover;
    min-height: 38rem;
    width: 100%;
    z-index: 9;


    .title {
        // background-color: rgba(211, 211, 211, 0.3);
        width: 100%;
        min-height: 32.5rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-size: 4rem;
    }

}
</style>