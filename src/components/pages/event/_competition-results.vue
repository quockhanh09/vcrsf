<template>
  <section>
    <div
      class="overlay relative h-[100px] tablet:h-[300px] flex justify-center items-center"
    >
      <div class="absolute w-full h-full -z-20">
        <img class="w-full h-full" :src="ketquaImg" alt="Kết quả thi đấu img" />
      </div>
      <div class="">
        <h3 class="container text-yellow">
          {{ t('competition-results') }}
        </h3>
      </div>
    </div>
  </section>
  <Events :newStatus="'Đã diễn ra'" />
</template>

<script setup>
import { defineAsyncComponent } from 'vue';
import ketquaImg from '@/assets/images/su-kien-sap-dien-ra.jpeg';
import { useI18n } from 'vue-i18n';
const Events = defineAsyncComponent(() => import('./events.vue'));
const { t } = useI18n();
</script>

<style scoped></style>
