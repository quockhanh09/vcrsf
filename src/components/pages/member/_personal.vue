<template>
  <section>
    <div
      class="overlay relative h-[100px] tablet:h-[300px] flex justify-center items-center"
    >
      <div class="absolute w-full h-full -z-20">
        <img class="w-full h-full" :src="memberImg" alt="member img" />
      </div>
      <div>
        <h3 class="text-[26px] tablet:text-[48px] text-center text-lightYellow">
          {{ t(`${currSlide}`) }}
        </h3>
      </div>
    </div>
  </section>
  <section>
    <ul
      class="flex justify-between text-[10px] tablet:text-xl font-bold uppercase"
    >
      <li
        class="w-1/3 border-b-[2px] border-borderGray"
        :class="currSlide === 'athletes' ? 'active' : ''"
        @click="changeSlides('athletes')"
      >
        {{ t('athletes') }}
      </li>
      <li
        class="w-1/3 border-b-[2px] border-borderGray"
        :class="currSlide === 'coach' ? 'active' : ''"
        @click="changeSlides('coach')"
      >
        {{ t('coach') }}
      </li>
      <li
        class="w-1/3 border-b-[2px] border-borderGray"
        :class="currSlide === 'referees' ? 'active' : ''"
        @click="changeSlides('referees')"
      >
        {{ t('referees') }}
      </li>
    </ul>
  </section>
  <section class="container my-16">
    <!-- <transition name="slide-translate" mode="out-in"> -->
    <AthletesPreview v-if="currSlide === 'athletes'" />
    <CoachPreview v-else-if="currSlide === 'coach'" />
    <RefereesPreview v-else-if="currSlide === 'referees'" />
    <!-- </transition> -->
  </section>
</template>

<script setup>
import memberImg from '@/assets/images/van-dong-vien.jpeg';
import { defineAsyncComponent, ref } from 'vue';
import { useI18n } from 'vue-i18n';
const AthletesPreview = defineAsyncComponent(() =>
  import('@/components/preview/_athletes-preview.vue')
);
const CoachPreview = defineAsyncComponent(() =>
  import('@/components/preview/_coach-preview.vue')
);
const RefereesPreview = defineAsyncComponent(() =>
  import('@/components/preview/_referees-preview.vue')
);
const { t } = useI18n();
const currSlide = ref('athletes');
const changeSlides = (slide) => {
  currSlide.value = slide;
};
</script>

<style scoped>
li {
  cursor: pointer;
  padding: 25px 0 12px 0;
  display: flex;
  justify-content: center;
  transition: all 0.2s linear;
}
li:hover {
  border-bottom: 5px solid rgba(255, 222, 47, 1);
  color: rgba(255, 222, 47, 1);
}
.active {
  border-bottom: 5px solid rgba(255, 222, 47, 1);
  color: rgba(255, 222, 47, 1);
}
</style>
