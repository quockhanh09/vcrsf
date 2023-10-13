<template>
  <section class="h-[184px] tablet:h-[680px] text-white">
    <Carousel class="carousel" v-slot="{ currentSlide }">
      <Slide v-for="slide in carouselSlides" :key="slide.id">
        <div v-show="currentSlide === slide.id" class="slide">
          <div class="slide-info">
            <img
              class="w-full h-full"
              v-lazy="slide.imgUrl"
              :alt="`slide images ${slide.imgUrl}`"
            />
          </div>
          <div class="absolute w-full h-full -z-10">
            <img
              class="w-full h-full"
              v-lazy="linearImg"
              :alt="`slide images`"
            />
          </div>
          <div
            class="container h-full flex flex-col justify-center items-start gap-[20px]"
          >
            <h1 class="2/3">
              {{ slide.name }}
            </h1>
            <p class="w-1/2 min-h-[137px] text-start">{{ slide.desc }}</p>
            <button class="my-[20px] btn btn-view-more">
              {{ t("view-more") }}
            </button>
          </div>
        </div>
      </Slide>
    </Carousel>
  </section>

  <section
    class="h-full w-full  flex flex-col justify-center items-center tablet:h-[380px] "
  >
    <div class="event-banner flex flex-col justify-center items-center tablet:h-[280px] tablet:w-[1000px]" :style="`background-image: url(${timeImg});`">
      <h3 class="text-yellow">{{ eventName }}</h3>
      <p><i class="fa-regular fa-clock"></i>Thời gian sự kiện:</p>
      <div class="countdown">
        <div class="countdown-item">
          <span class="num-count">{{ days }}</span>
          <p class="date-item">Ngày</p>
        </div>
        <div class="countdown-item">
          <span>{{ hours }}</span>
          <p class="date-item">Giờ</p>
        </div>
        <div class="countdown-item">
          <span>{{ minutes }}</span>
          <p class="date-item">Phút</p>
        </div>
        <div class="countdown-item">
          <span>{{ seconds }}</span>
          <p class="date-item">Giây</p>
        </div>
      </div>
    </div>
  </section>
</template>
<!-- 
sửa thêm là số thời gian với chữ thành dạng cột , số ở trên  -->
<script setup>
import Carousel from "./carousel/carousel.vue";
import Slide from "./carousel/slide.vue";
import defaultImg from "@/assets/images/_Banner.png";
import linearImg from "@/assets/images/linear.png";
import timeImg from "@/assets/images/default.png";
import { useI18n } from "vue-i18n";
const { t } = useI18n();

import { ref, computed, watch } from "vue";

const eventName = ref("Giải đua thuyền canoeing quốc gia 2023 ");
const eventDate = new Date("2023-12-31T23:59:59");

const days = computed(() => {
  const now = new Date();
  const timeDiff = eventDate - now;
  return Math.floor(timeDiff / (1000 * 60 * 60 * 24));
});

const hours = computed(() => {
  const now = new Date();
  const timeDiff = eventDate - now;
  return Math.floor((timeDiff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
});

const minutes = computed(() => {
  const now = new Date();
  const timeDiff = eventDate - now;
  return Math.floor((timeDiff % (1000 * 60 * 60)) / (1000 * 60));
});

const seconds = computed(() => {
  const now = new Date();
  const timeDiff = eventDate - now;
  return Math.floor((timeDiff % (1000 * 60)) / 1000);
});
const carouselSlides = [
  {
    id: 1,
    imgUrl: defaultImg,
    name: "JUNE 2023: RAPHAEL AHUMADA IRELAND",
    desc: "Lorem ipsum dolor sit amet consectetur. Turpis sit risus ipsum cursus nulla fringilla risus vitae et. Vitae sapien odio tristique.Lorem ipsum dolor sit amet consectetur. Turpis sit risus ipsum cursus nulla fringilla risus vitae et. Vitae sapien odio tristique.",
  },
  {
    id: 2,
    imgUrl: defaultImg,
    name: "JUNE 2024: RAPHAEL AHUMADA",
    desc: "Lorem ipsum dolor sit amet consectetur. Turpis sit risus ipsum cursus nulla fringilla risus vitae et. Vitae sapien odio tristique.",
  },
  {
    id: 3,
    imgUrl: defaultImg,
    name: "JUNE 2025: RAPHAEL AHUMADA IRELAND",
    desc: "Lorem ipsum dolor sit amet consectetur. Turpis sit risus ipsum cursus nulla fringilla risus vitae et. Vitae sapien odio tristique.Lorem ipsum dolor sit amet consectetur. Turpis sit risus ipsum cursus nulla fringilla risus vitae et. Vitae sapien odio tristique.",
  },
];
</script>

<style scoped>
.carousel {
  position: relative;
  height: 100%;
}
.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  max-height: 100%;
  height: 100%;
  transition: all 0.3s linear;
}
.slide-info {
  background: linear-gradient(
    90deg,
    rgba(16, 86, 184, 0.9) 0%,
    rgba(56, 113, 193, 0.2) 52.08%,
    rgba(56, 113, 193, 0) 99.48%
  );
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -20;
}
.event-banner {
  background-size: cover;
  background-repeat: no-repeat;
  color: #ffffff;
  padding: 20px;
  text-align: center;
  background-position: center;
  border-radius: 10px;
}

.countdown {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  margin-top: 10px;
}

.countdown-item {
  text-align: center;
  margin: 0 20px;
}

h3 {
  text-align: center;
}
.date-item{
  font-size: small;
}
.countdown span {
  display: block;
  position: relative;
  font-size: 3.5em;
}

.countdown span::before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: #007bff;
  animation: wave 1.5s ease-in-out infinite;
}

@keyframes wave {
  0%, 100% {
    transform: translateY(0);
  }
  25% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(0px);
  }
  75% {
    transform: translateY(0px);
  }
}
</style>
