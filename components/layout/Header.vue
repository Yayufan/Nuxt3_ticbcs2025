<template>
    <header class="header">
        <div class="title" v-if="title != ''">
            <p>{{ title.split('(')[0] }}</p>
            <p>{{ title.split('y')[1] }}</p>
        </div>
        <!-- <div class="hamburger-icon">
            <div class="container">
                <div class="hamburger" :class="{ 'is-active': isActive }" id="hamburger-1" @click="openMenu">
                    <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                    <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                    <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                </div>

            </div>
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


const openMenu = () => {
    isActive.value = !isActive.value;
    emits('openMenu', isActive.value);
}

const closeMenu = () => {
    isActive.value = false;
    emits('openMenu', isActive.value);
}

const emits = defineEmits(['openMenu']);

const headToMemberCenter = () => {
    console.log('headToMemberCenter');
    router.push('/member-center');
}

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
    background: url('/img/ticbcsBanner.png') no-repeat center center;
    background-size: cover;
    min-height: 32.5rem;
    width: 100%;

    top: 0;
    left: 0;
    z-index: 9;
    .title {
        background-color: rgba(211, 211, 211, 0.3);
        width: 100%;
        // opacity: 0.6;
        border: 1px solid red;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        font-size: 4rem;
    }

    .hamburger-icon {
        position: absolute;
        left: 0;
        top: -0.8rem;
        display: none;
        padding: 20px;




        .hamburger .line {
            width: 1.5rem;
            height: 3px;
            background-color: #000;
            margin-top: 5px;
            display: block;
            -webkit-transition: all 0.3s ease-in-out;
            -o-transition: all 0.3s ease-in-out;
            transition: all 0.3s ease-in-out;



            &:hover {
                cursor: pointer;
            }

            &.is-scroll {
                background-color: white !important;
            }
        }

        #hamburger-1.is-active .line:nth-child(2) {
            background-color: white;
            opacity: 0;
        }

        #hamburger-1.is-active .line:nth-child(1) {
            background-color: white;
            transform: 0.5s;

            rotate: 360deg;
            -webkit-transform: translateY(7.9px) rotate(47deg);
            -ms-transform: translateY(7.9px) rotate(47deg);
            -o-transform: translateY(7.9px) rotate(47deg);
            transform: translateY(7.9px) rotate(47deg);
            border-radius: 3px;
        }

        #hamburger-1.is-active .line:nth-child(3) {
            background-color: white;
            transform: 0.5s;
            rotate: 360deg;


            -webkit-transform: translateY(-8.4px) rotate(-47deg);
            -ms-transform: translateY(-8.4px) rotate(-47deg);
            -o-transform: translateY(-8.4px) rotate(-47deg);
            transform: translateY(-8.4px) rotate(-47deg);
            border-radius: 3px;
        }

    }

    .user-icon {
        width: 2rem;
        position: absolute;
        display: none;
        right: 4rem;
        top: 2.1rem;
        z-index: 10;

        img {
            width: 100%;
        }
    }



    @media screen and (max-width: 468px) {
        .hamburger-icon {
            display: block;
        }

        .user-icon {
            display: block;
        }

    }
}
</style>