<template>
  <div class="mb-16">
    <div
      class="overlay relative h-[100px] tablet:h-[300px] flex justify-center items-center"
    >
      <div class="absolute w-full h-full -z-20">
        <img class="w-full h-full" v-lazy="vanbanImg" alt="Văn bản img" />
      </div>
      <div class="container">
        <h3
          class="text-[26px] tablet:text-[48px] text-center text-lightYellow uppercase"
        >
          {{ t('legal-doc') }}
        </h3>
      </div>
    </div>
  </div>
  <div class="container my-16">
    <div>
      <div class="flex justify-between items-center">
        <div class="relative">
          <select
            class="cursor-pointer"
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
            class="search-item"
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
    </div>
    <div class="my-8">
      <transition name="slide-translate" mode="out-in">
        <table v-if="!loadingDocs" class="text-[10px] tablet:text-base">
          <tr>
            <th>{{ t('doc-name') }}</th>
            <th>{{ t('update-day') }}</th>
            <th>{{ t('attached-file') }}</th>
          </tr>
          <tr v-for="doc in docs" :key="doc.id">
            <td>
              {{ doc.name }}
            </td>
            <td>{{ doc.create_at }}</td>
            <td>
              <img
                class="cursor-pointer w-[12px] tablet:w-[24px] h-[12px] tablet:h-[24px]"
                v-lazy="downLoadFileIc"
                alt="download file"
                @click="() => handleDownload(doc.uploaded_file, doc.name)"
              />
            </td>
          </tr>
        </table>
      </transition>
    </div>
    <div class="btn view-more flex justify-center">
      <button @click="loadMore">{{ t('view-more') }}</button>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useI18n } from 'vue-i18n';
import vanbanImg from '@/assets/images/van-ban.jpeg';
import downArrowIc from '@/assets/images/down-line.svg';
import searchIc from '@/assets/images/tabler_search.svg';
import downLoadFileIc from '@/assets/images/library/downfile.png';
import getDocs from '@/composables/getDocs.js';
import handleDownload from '@/composables/downloadFile.js';
const { t } = useI18n();
const arrangeValue = ref('-');
const searchValue = ref('');
const {
  docs,
  loadingDocs,
  fetchDataDocs,
  loadMore,
  handleArrange,
  handleSearch,
} = getDocs('texts');
onMounted(async () => {
  await fetchDataDocs();
});
</script>

<style></style>
