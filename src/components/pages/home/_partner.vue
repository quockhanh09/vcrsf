<template>
  <section class="container flex flex-col gap-[40px]">
    <div class="relative">
      <h2 class="w-full">{{ t('partner') }}</h2>
      <div class="absolute top-0 right-0 flex">
        <arrow-right-ic @click="prev()" />
        <arrow-left-ic @click="next()" />
      </div>
    </div>
    <transition name="slide-translate" mode="out-in">
      <div
        v-if="!loadingPartners"
        class="flex justify-between items-center flex-wrap gap-[10px] tablet:gap-[40px]"
      >
        <img
          class="partner img w-[100px] tablet:w-[200px] h-[100px] tablet:h-[200px] rounded-full object-contain"
          v-for="partner in partners"
          :key="partner?.id"
          v-lazy="partner?.image"
          :alt="partner?.name"
        />
      </div>
    </transition>
  </section>
</template>

<script setup>
import { useI18n } from 'vue-i18n';
import { onMounted, ref } from 'vue';
import getPartners from '@/composables/getPartners.js';
import arrowLeftIc from '@/assets/icons/arrow-left.vue';
import arrowRightIc from '@/assets/icons/arrow-right.vue';
const { t } = useI18n();
const activeSlide = ref(1);
const { partners, total, loadingPartners, fetchDataPartners, loadMore } =
  getPartners(4);
onMounted(async () => {
  await fetchDataPartners();
});

const prev = async () => {
  if (activeSlide.value === 1) {
    return;
  } else {
    activeSlide.value -= 1;
  }
  await loadMore(activeSlide.value);
};
const next = async () => {
  if (activeSlide.value === total.value) {
    return;
  } else {
    activeSlide.value += 1;
  }
  await loadMore(activeSlide.value);
};
</script>

<style scoped></style>
