<template>
  <section class="container flex flex-col gap-[40px]">
    <div>
      <h2>{{ t('news') }}</h2>
    </div>
    <div>
      <Carousel :breakpoints="breakpoints">
        <Slide v-for="news in relatedNews" :key="news.id">
          <NewsPreview :news="news" />
        </Slide>
      </Carousel>
    </div>
    <div class="flex justify-center items-center">
      <button
        class="btn btn-view-more"
        @click="() => router.push({ name: 'News' })"
      >
        {{ t('view-more-news') }}
      </button>
    </div>
  </section>
</template>

<script setup>
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';
import { onMounted } from 'vue';
import { useI18n } from 'vue-i18n';
import getRelatedNews from '@/composables/getRelatedNews.js';
import NewsPreview from '@/components/preview/_news-preview.vue';
import { useRouter } from 'vue-router';
const router = useRouter();
const { relatedNews, fetchDataRelated } = getRelatedNews('', '');
onMounted(async () => {
  await fetchDataRelated();
});
const { t } = useI18n();
const breakpoints = {
  // 480px and up
  480: {
    mouseDrag: false,
    wrapAround: true,
    transition: 500,
    autoplay: 3000,
    itemsToShow: 2,
    snapAlign: 'center',
  },
  // 1024 and up
  1024: {
    mouseDrag: false,
    wrapAround: true,
    transition: 500,
    autoplay: 3000,
    itemsToShow: 4,
    snapAlign: 'start',
  },
};
</script>

<style scoped>
.carousel__slide {
  padding: 0;
  scroll-snap-stop: auto;
  flex-shrink: 0;
  margin: 0;
  /* position: relative; */

  display: flex;
  justify-content: center;
  align-items: center;

  /* Fix iOS scrolling #22 */
  transform: translateZ(0);
}
</style>
