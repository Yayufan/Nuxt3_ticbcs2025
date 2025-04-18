<template>
    <section class="top-section">
        <div class="menu-container" :class="[{ 'menu-section-scroll': isScroll }, { 'is-active': isActive }]">

            <div class="hamburger-icon">
                <div class="container">
                    <div class="hamburger" :class="{ 'is-active': isActive }" id="hamburger-1" @click="openMenu">
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                    </div>
                </div>
            </div>

            <div class="logo-container" v-if="!isActive">
                <nuxt-link class="logo-link" to="/conference-information"
                    @click="setActiveItem('conferenceInformation')">
                    <div class="logo-image-box">
                        <img class="logo" src="/img/logo.png" alt="TICBCS Logo" />
                    </div>
                    <h2 class="logo-title">2025 TICBCS</h2>
                </nuxt-link>
            </div>

            <div class="menu-box">

                <nuxt-link class="menu-item" to="/conference-information"
                    @click="setActiveItem('conferenceInformation')"
                    :class="activeClass('conferenceInformation')">會議資訊</nuxt-link>
                <nuxt-link class="menu-item" to="/seminar-registration" @click="setActiveItem('seminarRegistration')"
                    :class="activeClass('seminarRegistration')">研討會報名</nuxt-link>
                <nuxt-link class="menu-item" to="/credit-application" @click="setActiveItem('creditApplication')"
                    :class="activeClass('creditApplication')">學分申請</nuxt-link>

                <div class="item-box">
                    <nuxt-link class="menu-item" to="/sponsor-list" @click="setActiveItem('sponsorList')"
                        :class="activeClass('sponsorList')">贊助廠商</nuxt-link>
                    <nuxt-link class="menu-item" to="/mascot" @click="setActiveItem('mascot')"
                        :class="activeClass('mascot')">吉祥物專區</nuxt-link>
                    <nuxt-link class="menu-item" to="/gallery" @click="setActiveItem('gallery')"
                        :class="activeClass('gallery')">Gallery(2023
                        TICBCS)</nuxt-link>
                </div>

                <div class="sub-menu-box">
                    <div class="sub-menu-title" @click="toggleMenu">查看更多<el-icon>
                            <ElIconArrowDown />
                        </el-icon></div>
                    <div class="sub-menu-item-box" v-if="isOpen">
                        <nuxt-link class="sub-menu-item" to="/sponsor-list" @click="setActiveItem('sponsorList')"
                            :class="activeClass('sponsorList')">贊助廠商</nuxt-link>
                        <nuxt-link class="sub-menu-item" to="/mascot" @click="setActiveItem('mascot')"
                            :class="activeClass('mascot')">吉祥物專區</nuxt-link>
                        <nuxt-link class="sub-menu-item" to="/gallery" @click="setActiveItem('gallery')"
                            :class="activeClass('gallery')">Gallery(2023TICBCS)</nuxt-link>
                    </div>
                </div>

            </div>


        </div>
    </section>
</template>

<script lang="ts" setup>

// 偵測滾輪位置，更換 menu 背景色
const isScroll = ref(false)
function handleScroll() {
    let scrollPositionY = window.scrollY
    if (scrollPositionY > 0) {
        isScroll.value = true
    } else {
        isScroll.value = false
    }
}

const isOpen = ref(false)
const toggleMenu = () => {
    isOpen.value = !isOpen.value
}

const activeItem = ref('conferenceInformation')
const setActiveItem = (item: string) => {
    activeItem.value = item
    isOpen.value = false
    console.log('activeItem', activeItem.value)
}

const activeClass = (item: string) => {
    return activeItem.value === item ? 'active' : ''
}

/**================================================================ */

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







/**================================================================ */
onMounted(() => {
    window.addEventListener('scroll', handleScroll)
})

</script>
<style lang="scss" scoped>
.top-section {

    .menu-container {
        display: flex;
        position: fixed;
        top: 0;
        z-index: 99;
        width: 100%;
        height: 3rem;
        padding: 0.8rem;

        &.is-active {
            width: 10%;
            height: 2.5rem;
        }

        .logo-container {
            width: 35%;
            height: 100%;

            .logo-link {
                width: 100%;
                height: 100%;
                cursor: pointer;
                display: flex;
                text-align: center;
                justify-content: flex-start;
                align-items: center;
                gap: 0.8rem;

                .logo-image-box {
                    width: 7rem;

                    .logo {
                        width: 100%;
                        height: 100%;
                        object-fit: cover;
                        object-position: center;
                    }
                }
                

                .logo-title {
                    font-size: 1.5rem;
                    color: #59413C;
                }
            }

            @media screen and (max-width: 468px) {
                margin-left: 1rem;
            }

            @media screen and (max-width: 769px) {
                .logo-title {
                    display: none;
                }
            }
        }

        .menu-box {
            width: 65%;
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding-right: 1.5rem;
            gap: 1.5rem;
            font-size: 1rem;


            .active {
                color: black;
            }

            .item-box {
                display: flex;
                gap: 1.5rem;
            }

            .menu-item {
                color: #59413C;
                text-decoration: none;

                &:hover {
                    cursor: pointer;
                    color: black;
                }
            }

            .sub-menu-box {
                display: none;
                color: #59413C;
                text-decoration: none;
                position: relative;

                .sub-menu-title {
                    display: flex;
                    align-items: center;
                    gap: 0.1rem;
                }

                .sub-menu-item-box {
                    display: flex;
                    flex-direction: column;
                    position: absolute;
                    gap: 1rem;
                    top: 3rem;
                    right: -0.5rem;
                    background-color: black;
                    padding: 1rem 1.5rem;
                    border-radius: 0.5rem;
                    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
                    z-index: 1000;

                    .active {
                        color: #FF5529;
                    }

                    .sub-menu-item {
                        color: white;

                        &:active {
                            color: #FF5529;
                        }
                    }
                }
            }


            

            @media screen and (max-width: 1024px) {
                width: 70%;
                padding-right: 0;
                gap: 0.5rem;

                .item-box {
                    gap: 0.5rem;
                }
                
            }


            @media screen and (max-width: 769px) {
                width: 70%;

                .item-box {
                    display: none;
                }

                .sub-menu-box {
                    display: flex;
                }
            }

            @media screen and (max-width: 468px) {
                display: none;
            }
        }
    }

    .menu-section-scroll {
        background-color: black;
        transition: background-color 0.3s ease-in-out;


        .logo-container {

            .logo-link {

                .logo-title {
                    color: white;
                }
            }
        }

        .menu-box {
            .menu-item {
                color: white;

                &:hover {
                    cursor: pointer;
                    color: #FF5529;
                }
            }

            .active {
                color: #FF5529;
            }

            .sub-menu-box {
                font-size: 1rem;
                color: white;
                text-decoration: none;

                .sub-menu-item-box {
                    .active {
                        color: #FF5529 !important;
                    }
                }

            }
        }
    }


    // 測試
    .hamburger-icon {
        display: none;

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

        @media screen and (max-width: 469px) {
            display: block;



        }

    }
}
</style>