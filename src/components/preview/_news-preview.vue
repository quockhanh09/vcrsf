<template>
  <article
    class="w-[305px] mx-[10px] bg-lightBlue flex flex-col items-start gap-[20px]"
  >
    <div class="w-full">
      <img
        class="w-full h-[100px] tablet:h-[185px] item-img"
        v-lazy="news?.image"
        :alt="news?.title"
      />
    </div>
    <div class="px-[12px] flex flex-col items-start gap-[12px]">
      <div>
        <p class="italic text-sm">
          {{ formatDay(news?.publication_date) }}
        </p>
      </div>
      <div>
        <h3 class="text-[10px] tablet:text-[22px]">
          {{
            news?.title.length > 12
              ? news?.title.substring(0, 12) + '...'
              : news?.title
          }}
        </h3>
      </div>
      <div class="h-[57px] text-start">
        <p class="text-[8px] tablet:text-base">
          {{
            news?.description.length > 100
              ? news?.description.substring(0, 100) + '...'
              : news?.description
          }}
        </p>
      </div>
      <div class="my-[10px]">
        <button
          class="relative text-[14px] text-blue"
          @click="
            () =>
              router.push({
                name: 'NewsDetails',
                params: { id: news.id, category: news.category },
              })
          "
        >
          {{ t('read-more') }}
        </button>
      </div>
    </div>
  </article>
</template>
<script setup>
import { useI18n } from 'vue-i18n';
import { formatDay } from '@/plugins/date-utils';
import { useRouter } from 'vue-router';
const props = defineProps({
  news: Object,
});
const { t } = useI18n();
const router = useRouter();
</script>

<style scoped>
button::before {
  position: absolute;
  content: '';
  bottom: 0;
  left: 0;
  width: 57px;
  height: 1px;
  background-color: #3871c1;
}
</style>
