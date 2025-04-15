<template>
    <div class="common-section">
        <div class="meeting-info">
            <h1 class="title">研討會資訊</h1>
            <div class="meeting-info-box">
                <p><span class="title">主辦單位:</span>中國醫藥大學、中國醫藥大學附設醫院、中華民國乳癌教育暨防治學會</p>
                <p><span class="title">指導單位:</span>台灣乳房醫學會、台灣外科醫學會</p>
                <div>
                    <p><span class="title">會議時間:</span>2024年06月22日(六)，上午09:00 - 下午06:05
                    </p>
                    <p class="time">
                        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                        2024年06月23日(日)，上午08:50 - 下午12:10</p>
                </div>
                <p><span class="title">會議地點:</span>中國醫藥大學水湳校區 卓越大樓B2 國際會議廳 (406台中市北屯區經貿路一段100號)</p>
            </div>
        </div>

        <div class="agenda-info">
            <h1 class="title">Agenda</h1>
            <div class="agenda-info-box">
                <img src="../assets/img/2024-TICBCS-agenda.png" alt="">
                <a href="https://drive.google.com/drive/folders/1RCUQwuiVAU6WWkYZll8Q4Z7GE2GYQ1ZP" target="_blank"
                    class="agenda-download">
                    TICBCS 議程下載
                </a>
            </div>
        </div>

        <div class="registration">
            <a href="" class="download">
                <img src="../assets/img/ticbcs_registration.png" alt="">
            </a>
        </div>
        <div class="location">
            <h1 class="title">會議地點: <span class="location-info">中國醫藥大學水湳校區  卓越大樓B2 國際會議廳 (406台中市北屯區經貿路一段100號)</span></h1>
            <div class="location-info-box">
                <iframe
                    src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d3639.807528415075!2d120.66119900000001!3d24.178482!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x346916320ec920ed%3A0xc60ae710ee7eef57!2zNDA35Y-w54Gj5Y-w5Lit5biC5YyX5bGv5Y2A57aT6LK_6Lev5LiA5q61MTAw6Jmf!5e0!3m2!1szh-TW!2sus!4v1744600773772!5m2!1szh-TW!2sus"
                    frameborder="0"></iframe>
            </div>
        </div>


    </div>
</template>
<script setup lang="ts">

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

    .meeting-info {
        border-width: 1px 0 1px 0;
        border-style: solid;
        border-color: #D3D3D3;
        width: 100%;
        padding: 1.5rem 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        .meeting-info-box {
            width: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: flex-start;
            font-size: 1.5rem;
            line-height: 2rem;
            gap: 1rem;


            .title {
                font-weight: bold;
                font-size: 1.5rem;
                margin-right: 1rem;
            }
        }
    }

    .agenda-info {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;


        img {
            width: 100%;
        }

        .agenda-download {
            background-color: #FF5529;
            display: block;
            margin: 2rem auto 0 auto;
            padding: 0.5rem 0;
            color: black;
            border: 1px solid black;
            border-radius: 0.3rem;
            text-align: center;
            width: 50%;

            &:hover {
                box-shadow: 0 1px 5px rgba(0, 0, 0, 0.5);
            }
        }
    }

    .registration {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        padding: 2.5rem 0;
        border-width: 1px 0 1px 0;
        border-style: solid;
        border-color: #D3D3D3;

        .download {
            width: 80%;
            display: flex;
            justify-content: center;
            align-items: center;

            img {
                width: 100%;
                height: 100%;
            }
        }
    }

    .location {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        width: 100%;
        padding: 2.5rem 0;
        border-width: 0px 0 1px 0;
        border-style: solid;
        border-color: #D3D3D3;

        .location-info {
            font-size: 1.2rem;
            font-weight: normal;
        }

        .location-info-box {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;

            iframe {
                width: 100%;
                height: 30rem;
                border-radius: 0.5rem;
            }
        }
    }
}
</style>