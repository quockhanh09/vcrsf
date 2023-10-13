<template>
  <section
    class="overlay relative h-[100px] tablet:h-[300px] flex justify-center items-center"
  >
    <div class="absolute w-full h-full -z-20">
      <img class="w-full h-full" v-lazy="contactImg" alt="contact img" />
    </div>
    <div>
      <h3 class="container text-yellow">{{ t('alliance') }}</h3>
    </div>
  </section>
  <transition name="slide-translate" mode="out-in">
    <section
      v-if="!loadingPartners"
      class="container my-8 flex flex-col gap-[20px]"
    >
      <div
        v-for="partner in partners"
        :key="partner?.id"
        class="flex justify-start items-center gap-[5px] tablet:gap-[40px] border-b border-borderGray"
      >
        <div>
          <img
            class="w-[40px] tablet:w-[130px] h-[40px] tablet:h-[130px] tablet:rounded-full object-contain"
            v-lazy="partner?.image"
            :alt="partner?.name"
          />
        </div>
        <div>
          <div>
            <h4 class="text-2xl font-bold">{{ partner?.name }}</h4>
          </div>
          <div class="my-4">
            <p class="text-gray font-bold">
              {{ partner?.address }}
            </p>
          </div>
          <div class="flex gap-[40px]">
            <div class="flex items-center gap-[10px]">
              <img v-lazy="basePhoneIc" alt="base phone ic" />
              <p>{{ partner?.phone }}</p>
            </div>
            <div class="flex items-center gap-[10px]">
              <img v-lazy="emailIc" alt="email ic" />
              <p>{{ partner?.email }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </transition>
  <section v-if="partners.length" class="my-16">
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
import { useI18n } from 'vue-i18n';
import { onMounted, ref } from 'vue';
import VPagination from '@hennge/vue3-pagination';
import '@hennge/vue3-pagination/dist/vue3-pagination.css';
import contactImg from '@/assets/images/contact/contact.jpg';
import basePhoneIc from '@/assets/images/contact/baseline-phone.png';
import emailIc from '@/assets/images/contact/email.png';
import getPartners from '@/composables/getPartners';
const { t } = useI18n();
const count = ref(1);
const { partners, total, loadingPartners, fetchDataPartners } = getPartners(6);
onMounted(async () => {
  await fetchDataPartners();
});
</script>

<style></style>
