<template>
  <main class="flex flex-col gap-[60px]">
    <HomeBanner />

    <HomeEvents />
    <HomeNews />
    <HomePartner />
  </main>
</template>

<script setup>
import { defineAsyncComponent } from 'vue';
const HomeBanner = defineAsyncComponent(() =>
  import('@/components/pages/home/_banner.vue')
);

const HomeEvents = defineAsyncComponent(() =>
  import('@/components/pages/home/_events.vue')
);
const HomeNews = defineAsyncComponent(() =>
  import('@/components/pages/home/_news.vue')
);
const HomePartner = defineAsyncComponent(() =>
  import('@/components/pages/home/_partner.vue')
);
</script>

<style scoped></style>
