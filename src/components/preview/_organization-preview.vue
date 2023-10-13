<template>
  <section class="flex justify-between items-center">
    <div class="relative">
      <select
        class="cursor-pointer"
        id="filter"
        v-model="filtered"
        @change="handleFiltered(filtered)"
      >
        <option value="">Tất Cả</option>
        <option v-for="genre in genres" :key="genre.name" :value="genre.name">
          {{ genre.name }}
        </option>
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
  </section>
  <section class="mt-8 overflow-hidden">
    <transition name="slide-translate" mode="out-in">
      <div v-if="!loadingOrganization" class="list-member">
        <div
          class="relative w-full h-full flex items-end"
          v-for="organization in organizations"
          :key="organization?.id"
        >
          <img
            class="absolute w-full h-full -z-10"
            v-lazy="organization?.image"
            :alt="organization?.name_group"
          />
          <div
            class="w-full p-[10px] tablet:p-[20px] bg-black text-white flex justify-between items-center"
          >
            <div>
              <h4 class="text-[14px] tablet:text-[20px]">
                {{ organization?.name_group }}
              </h4>
              <p class="uppercase tablet:my-4 text-[10px] tablet:text-base">
                {{ organization?.subject.name }}
              </p>
            </div>
            <div
              class="cursor-pointer"
              @click="
                () =>
                  router.push({
                    name: 'OrganizationDetails',
                    params: { id: organization?.number_group },
                  })
              "
            >
              <img :src="arrowRightIc" alt="arrow right ic" />
            </div>
          </div>
        </div>
      </div>
    </transition>
  </section>
  <section class="my-16">
    <VPagination
      class="flex justify-center items-center"
      v-model="count"
      :pages="total"
      :range-size="0"
      active-color="rgba(26, 30, 34, 1)"
      @update:modelValue="loadMore(count)"
    />
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useRouter } from 'vue-router';
import { useI18n } from 'vue-i18n';
import VPagination from '@hennge/vue3-pagination';
import '@hennge/vue3-pagination/dist/vue3-pagination.css';
import downArrowIc from '@/assets/images/down-line.svg';
import searchIc from '@/assets/images/tabler_search.svg';
import arrowRightIc from '@/assets/images/arrow-right.svg';
import LoadingComponents from '@/components/structure/loading-components/loading-components.vue';
import getOrganization from '@/composables/getOrganization';
import getGenres from '@/composables/getGenres.js';
const { t } = useI18n();
const router = useRouter();
const filtered = ref('');
const searchValue = ref('');
const count = ref(1);
const {
  organizations,
  total,
  loadingOrganization,
  fetchDataOrganization,
  handleFiltered,
  handleSearch,
  loadMore,
} = getOrganization();
const { genres, fetchDataGenres } = getGenres('');
onMounted(async () => {
  await fetchDataOrganization();
  await fetchDataGenres();
});
</script>

<style scoped></style>
