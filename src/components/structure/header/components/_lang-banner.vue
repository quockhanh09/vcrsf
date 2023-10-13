<template>
  <div class="font-semiBold">
    <button
      class="w-[56px] h-[56px] tablet:w-[81px] tablet:h-[60px] bg-yellow py-[18px] px-[14px] uppercase"
      @click="toggleLang"
    >
      {{ currLang === 'vi' ? 'vi' : 'en' }}
    </button>
  </div>
</template>

<script setup>
import i18n from '@/plugins/i18n';
import { ref } from 'vue';

const currLang = ref(window.localStorage.getItem('lang') || 'vi');

const toggleLang = () => {
  currLang.value = currLang.value === 'vi' ? 'en' : 'vi';
  i18n.global.locale.value = currLang.value;
  window.localStorage.setItem('lang', i18n.global.locale.value);
};
</script>

<style scoped>
button {
  border: none;
}
</style>
