<template>
  <div>
    <div class="flex justify-between items-center">
      <div class="relative">
        <select
          id="filter"
          v-model="arrangeValue"
          @change="handleArrange(arrangeValue)"
        >
          <option value="-">Mới nhất</option>
          <option value="+">Cũ nhất</option>
        </select>
        <img class="down-arrow-ic" v-lazy="downArrowIc" alt="down arrow ic" />
      </div>
      <div class="relative">
        <input
          class="search-item text-[8px] tablet:text-base"
          id="search"
          type="text"
          placeholder="Nhập từ khóa tìm kiếm"
          v-model="searchValue"
          @keydown.enter="() => handleSearch(searchValue)"
        />
        <img
          class="search-img"
          v-lazy="searchIc"
          alt="search ic"
          @click="() => handleSearch(searchValue)"
        />
      </div>
    </div>
    <div class="mt-8 overflow-hidden">
      <transition name="slide-translate" mode="out-in">
        <div v-if="!loadingNews" class="list-news">
          <div v-for="newsDetails in news" :key="newsDetails.id">
            <NewsPreview :news="newsDetails" />
          </div>
        </div>
      </transition>
    </div>
    <div class="my-16" v-if="news.length !== 0">
      <VPagination
        class="flex justify-center items-center"
        v-model="count"
        :pages="total"
        :range-size="0"
        active-color="rgba(26, 30, 34, 1)"
        @update:modelValue="loadMore(count)"
      />
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useI18n } from 'vue-i18n';
import VPagination from '@hennge/vue3-pagination';
import '@hennge/vue3-pagination/dist/vue3-pagination.css';
import downArrowIc from '@/assets/images/down-line.svg';
import searchIc from '@/assets/images/tabler_search.svg';
import NewsPreview from '@/components/preview/_news-preview.vue';
import getNews from '@/composables/getNews.js';
const { t } = useI18n();
const arrangeValue = ref('-');
const searchValue = ref('');
const count = ref(1);
const {
  news,
  total,
  loadingNews,
  fetchDataNews,
  loadMore,
  handleArrange,
  handleSearch,
} = getNews('Tin tức trong nước');
onMounted(async () => {
  await fetchDataNews();
});
</script>

<style scoped></style>
