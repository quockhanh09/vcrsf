<template>
  <article class="container my-16">
    <section class="pb-4 border-b border-borderGray">
      <div>
        <p
          class="w-[150px] h-[30px] bg-opaBlack text-yellow flex justify-center items-center font-bold text-sm rounded-[5px]"
        >
          {{ newsDetails?.tag || 'tag' }}
        </p>
        <h1 class="my-4 text-[3rem]">{{ newsDetails?.title }}</h1>
      </div>
      <div class="flex justify-between items-center">
        <div>
          <p>{{ formatDate(newsDetails?.publication_date) }}</p>
        </div>
        <div class="flex items-center gap-[10px]">
          <p>Chia sẻ bài viết:</p>
          <ShareNetwork network="facebook" :url="shareUrl">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="20"
              height="20"
              viewBox="0 0 20 20"
              fill="none"
            >
              <path
                d="M20 10C20 4.48 15.52 0 10 0C4.48 0 0 4.48 0 10C0 14.84 3.44 18.87 8 19.8V13H6V10H8V7.5C8 5.57 9.57 4 11.5 4H14V7H12C11.45 7 11 7.45 11 8V10H14V13H11V19.95C16.05 19.45 20 15.19 20 10Z"
                fill="#797979"
              />
            </svg>
          </ShareNetwork>
        </div>
      </div>
    </section>
    <section class="text-xl">
      <div class="font-bold">
        {{ newsDetails?.header }}
      </div>
      <div>
        {{ newsDetails?.main }}
      </div>
      <div class="w-4/5 mx-auto my-4">
        <img
          class="w-full h-full"
          v-lazy="newsDetails?.images"
          :alt="newsDetails?.title"
        />
      </div>
      <div>
        {{ newsDetails?.footer }}
      </div>
    </section>
    <section class="my-8">
      <div>
        <h2>{{ t('related-news') }}</h2>
      </div>
      <div class="my-8 recent-news">
        <div v-for="newsDetails in relatedNews" :key="newsDetails.id">
          <NewsPreview :news="newsDetails" />
        </div>
      </div>
      <div class="btn view-more flex justify-center">
        <button @click="() => router.push({ name: 'news' })">
          {{ t('view-more-news') }}
        </button>
      </div>
    </section>
  </article>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { useI18n } from 'vue-i18n';
import { formatDate } from '@/plugins/date-utils';
import getNewsDetails from '@/composables/getNewsDetails.js';
import getRelatedNews from '@/composables/getRelatedNews.js';
import NewsPreview from '@/components/preview/_news-preview.vue';
const { t } = useI18n();
const route = useRoute();
const router = useRouter();
const newsId = ref(route.params.id);
const newsCategory = ref(route.params.category);
const { newsDetails, fetchData } = getNewsDetails(newsId.value);
const { relatedNews, fetchDataRelated } = getRelatedNews(
  newsCategory.value,
  newsId.value
);
const shareUrl = ref(window.location.href);
onMounted(async () => {
  await fetchData();
  await fetchDataRelated();
});
</script>

<style></style>
