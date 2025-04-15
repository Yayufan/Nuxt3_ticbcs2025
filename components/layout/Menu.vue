<template>
    <section class="top-section">
        <div class="menu-section" :class="[{ 'menu-section-scroll': isScroll }, { 'is-active': isActive }]">
            <!-- 測試 -->
            <div class="hamburger-icon">
                <div class="container">
                    <div class="hamburger" :class="{ 'is-active': isActive }" id="hamburger-1" @click="openMenu">
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                        <span class="line" :class="{ 'is-scroll': isScroll }"></span>
                    </div>

                </div>
            </div>
            <!-- 測試 -->


            <div class="logo-box" v-if="!isActive">
                <nuxt-link class="logo-link" to="/conference-information" @click="setActiveItem('conferenceInformation')">
                    <div class="img-box">
                        <img class="logo" src="/img/logo.png" alt="">
                    </div>
                    <h2>2024 TICBCS</h2>
                </nuxt-link>
            </div>
            <div class="other-menu">
                <nuxt-link to="/conference-information" @click="setActiveItem('conferenceInformation')"
                    :class="activeClass('conferenceInformation')">會議資訊</nuxt-link>
                <nuxt-link to="/seminar-registration" @click="setActiveItem('seminarRegistration')"
                    :class="activeClass('seminarRegistration')">研討會報名</nuxt-link>
                <nuxt-link to="/credit-application" @click="setActiveItem('creditApplication')"
                    :class="activeClass('creditApplication')">學分申請</nuxt-link>
                <div class="item-box">
                    <nuxt-link to="/sponsor-list" @click="setActiveItem('sponsorList')"
                        :class="activeClass('sponsorList')">贊助廠商</nuxt-link>
                    <nuxt-link to="/mascot" @click="setActiveItem('mascot')"
                        :class="activeClass('mascot')">吉祥物專區</nuxt-link>
                    <nuxt-link to="/gallery" @click="setActiveItem('gallery')"
                        :class="activeClass('gallery')">Gallery(2023
                        TICBCS)</nuxt-link>
                </div>
                <div class="menu">
                    <div class="menu-title" @click="toggleMenu">查看更多<el-icon>
                            <ElIconArrowDown />
                        </el-icon></div>
                    <div class="menu-item-box" v-if="isOpen">
                        <nuxt-link to="/sponsor-list" @click="setActiveItem('sponsorList')"
                            :class="activeClass('sponsorList')">贊助廠商</nuxt-link>
                        <nuxt-link to="/mascot" @click="setActiveItem('mascot')"
                            :class="activeClass('mascot')">吉祥物專區</nuxt-link>
                        <nuxt-link to="/gallery" @click="setActiveItem('gallery')"
                            :class="activeClass('gallery')">Gallery(2023
                            TICBCS)</nuxt-link>
                    </div>
                </div>
            </div>


        </div>
    </section>
</template>

<script lang="ts" setup>

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

    .menu-section {
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

        .logo-box {
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

                .img-box {
                    width: 7rem;

                    .logo {
                        width: 100%;
                        height: 100%;
                        // max-width: 4rem;
                        object-fit: cover;
                        object-position: center;
                    }
                }

                h2 {
                    font-size: 1.5rem;
                    color: #59413C;
                    font-weight: bold;

                    @media screen and (max-width: 468px) {
                        display: none;

                    }
                }
            }

            @media screen and (max-width: 468px) {
                margin-left: 1rem;;
            }
        }

        .other-menu {
            width: 65%;
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding-right: 1.5rem;
            gap: 1.5rem;

            @media screen and (max-width: 468px) {
                display: none;
            }

            .active {
                color: black;
            }

            .item-box {
                display: flex;
                gap: 1.5rem;
            }

            .menu {
                display: none;
                font-size: 1rem;
                color: #59413C;
                text-decoration: none;

                .menu-title {
                    display: flex;
                    align-items: center;
                    gap: 0.1rem;
                }

                .menu-item-box {
                    display: flex;
                    flex-direction: column;
                    position: absolute;
                    top: 4.3rem;
                    right: 0;
                    background-color: black;
                    padding: 1rem 1.5rem;
                    border-radius: 0.5rem;
                    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
                    z-index: 1000;

                    .active {
                        color: #FF5529;
                    }

                    a {
                        margin-bottom: 1rem;
                        color: white;

                        &:active {
                            color: #FF5529; // Change to your desired hover color
                        }

                        &:last-child {
                            margin-bottom: 0;
                        }
                    }
                }
            }


            a {
                font-size: 1rem;
                color: #59413C;
                text-decoration: none;

                &:hover {
                    cursor: pointer;
                    color: black; // Change to your desired hover color
                }
            }



            @media screen and (max-width: 769px) {
                width: 70%;

                .item-box {
                    display: none;
                }

                .menu {
                    display: flex;
                    ;
                }
            }
        }



    }

    .menu-section-scroll {
        background-color: black;
        transition: background-color 0.3s ease-in-out;


        .logo-box {

            .logo-link {


                h2 {
                    color: white;
                }
            }
        }

        .other-menu {
            a {
                color: white;

                &:hover {
                    cursor: pointer;
                    color: #FF5529;
                }
            }

            .active {
                color: #FF5529;
            }

            .menu {
                font-size: 1rem;
                color: white;
                text-decoration: none;

                .menu-item-box {
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