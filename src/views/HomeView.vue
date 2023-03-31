<template>
    <div class="container" ref="firstButton">

        <NavbarComp />

        <div class="main">
            <img src="@/assets/kinopoisk.png" alt="" class="main__title">
            <div class="main__slogan">Они должны что-то знать</div>
            <!-- <div class="main__clouds"></div> -->
            <div class="main__content">

                <swiper ref="swiper" :pagination="{
                    type: 'fraction',
                }" :navigation="true" :modules="modules" class="swiper mySwiper main__content-swiper">
                    <!-- eslint-disable -->
                    <div slot="container-start" class="parallax-bg" data-swiper-parallax="-0%"></div>

                    <swiper-slide v-for="item in items" :key="item.id">
                        <img :src="item.image" alt="" class="main__content-swiper-img">
                        <div class="main__content-swiper-text" data-swiper-parallax="-300">{{ item.text }}
                        </div>
                    </swiper-slide>

                    <button @click="next()" class="swiper-button-next" style="opacity: 0;"></button>
                    <button @click="prev()" class="swiper-button-prev" style="opacity: 0;"></button>
                </swiper>

                <div class="main__content-button">
                    <p>Искать промокод</p>
                    <img src="@/assets/arrow.png" alt="#" class="main__content-button-arrow">
                </div>
            </div>
        </div>

        <div class="link">hd.kinopoisk.ru</div>
    </div>

    <!-- Сделал второй свайпер, от которого понадобились невидимые кнопки и текст.
         При нажатии кнопки первого слайдера, активируется кнопка второго. Первый слайдер прокручивает Картинку за облаками.
         Второй прокручивает текст поверх облака.
         Без использования swiper'а можно было бы реализовать то же самое гораздо проще при помощи :has() либо z-index. 
         Но пришлось придумать необычное, пусть и костыльное решение. :) -->

    <div ref="secondButton">
        <swiper :pagination="{
            type: 'fraction',
        }" :navigation="true" :modules="modules" class="swiper mySwiper content-swiper_separate">
            <swiper-slide v-for="item in items" :key="item.id">
                <img :src="item.image" alt="" class="main__content-swiper-img" :style="{ visibility: 'hidden' }">
                <div class="main__content-swiper-text" data-swiper-parallax="-300">{{ item.text }}
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>

<script lang="ts">
import { ref } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import NavbarComp from '@/components/NavbarComp.vue';

import racer from '@/assets/racer.png'

import 'swiper/css';

import 'swiper/css/pagination';
import 'swiper/css/navigation';

import '@/assets/main.css';

import { Pagination, Navigation, Parallax } from 'swiper';

export default {
    components: {
        Swiper,
        SwiperSlide,
        NavbarComp,
    },
    data() {
        return {
            items: [
                {
                    id: 1,
                    image: racer,
                    text: "Для примера мы показали вам его лицо. В первой серии он прячется в подвале за мониторами, и пусть борода не собьёт вас с толку. Найдите героя и нажмите на паузу — ему не терпится отдать вам промокод."
                },
                {
                    id: 2,
                    image: racer,
                    text: "Для примера мы показали вам его лицо. В первой серии он прячется в подвале за мониторами, и пусть борода не собьёт вас с толку. Найдите героя и нажмите на паузу — ему не терпится отдать вам промокод."
                },
                {
                    id: 3,
                    image: racer,
                    text: "Для примера мы показали вам его лицо. В первой серии он прячется в подвале за мониторами, и пусть борода не собьёт вас с толку. Найдите героя и нажмите на паузу — ему не терпится отдать вам промокод."
                }
            ]
        }
    },
    methods: {
        next() {
            let sw = this.firstButton.querySelector(".swiper").swiper;
            let sw2 = this.secondButton.querySelector(".swiper").swiper;
            setTimeout(() => {
                let a = this.secondButton.querySelectorAll(".swiper-button-next");
                a[0].addEventListener('click', {}, sw2.slideNext())
                let b = this.firstButton.querySelectorAll(".swiper-button-next");
                b[0].addEventListener('click', {}, sw.slideNext())
            }, 100)
        },
        prev() {
            let sw = this.firstButton.querySelector(".swiper").swiper;
            let sw2 = this.secondButton.querySelector(".swiper").swiper;
            setTimeout(() => {
                let a = this.secondButton.querySelectorAll(".swiper-button-prev");
                a[0].addEventListener('click', {}, sw2.slidePrev())
                let b = this.firstButton.querySelectorAll(".swiper-button-prev");
                b[0].addEventListener('click', {}, sw.slidePrev())
            }, 100)
        }
    },
    setup() {
        const swiper = ref(null);
        const secondButton: any = ref(null);
        const firstButton: any = ref(null);

        return {
            modules: [Parallax, Pagination, Navigation],
            swiper,
            secondButton,
            firstButton
        };
    },
};
</script>

<style scoped>
.container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: row;

    position: absolute;
    width: 1440px;
    height: 700px;

    background: url(../assets/clouds-2.png) no-repeat, url(../assets/background.png) no-repeat;
    z-index: 500;
}

/* main */
.main {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: column;

    position: relative;
    left: 3.7rem;

    height: 700px;
}

.main__title {
    position: relative;
    right: 4.8rem;

    margin-top: 1.2rem;
    cursor: pointer;
    z-index: 1;
}

.main__slogan {
    position: relative;
    top: 1.5rem;
    right: 4.6rem;

    width: 790px;

    font-family: 'Futura';
    font-style: normal;
    font-weight: 700;
    font-size: 45px;
    line-height: 72px;

    text-align: center;
    letter-spacing: -0.692308px;
    text-transform: uppercase;

    color: #FFCC64;

    z-index: 1;
}

.main__content {
    position: relative;
    margin: 0 auto;
    width: 900px;
    height: 800px;
}

.main__content-swiper {
    position: relative;
    right: 4.5rem;

    margin-top: -.5rem;

    width: 900px;
    height: 500px;
    z-index: 0;
}

.main__content-swiper-img {
    position: absolute;
    top: 8.8rem;
    left: 16.5rem;
    overflow: hidden;

    pointer-events: none;
    z-index: 0;

    clip-path: polygon(50% 0%, 100% 0, 100% 100%, 61% 76%, 35% 77%, 0 100%, 0 0);
}

.main__content-swiper-text {
    position: absolute;
    bottom: 6.5rem;
    right: .5rem;
    font-size: 20px;
    font-weight: 300;
    line-height: 32px;

    text-align: center;
    letter-spacing: 0.4px;

    color: #000000;
    z-index: 7;
    display: none;
}

.main__content-button {
    display: flex;
    flex-direction: row;

    position: relative;
    left: 18.5rem;
    z-index: 1;

    cursor: pointer;
}

.main__content-button p {
    position: relative;
    bottom: 2.6rem;

    font-size: 15px;
    line-height: 18px;
    text-align: center;

    color: #333333;
    z-index: 1;
}

.main__content-button-arrow {
    position: relative;
    bottom: 2.1rem;
    left: 1.6rem;
    width: 3.41px;
    height: 30.37px;
    transform: rotate(-90deg);
    z-index: 1;
}

/* Здесь пожертвовал БЭМ. */
.content-swiper_separate {
    position: relative;
    right: 0.5rem;
    top: 9rem;
    margin-top: 6.8rem;

    width: 900px;
    height: 500px;
    z-index: 600;
    pointer-events: none;
}

/* Link */
.link {
    font-size: 14px;
    font-weight: 400;
    line-height: 15px;

    text-align: center;

    color: #333333;

    transform: rotate(90deg);
    transform: rotate(90deg);

    position: relative;
    left: 1rem;
}
</style>