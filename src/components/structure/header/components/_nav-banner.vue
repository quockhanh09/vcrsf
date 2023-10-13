<template>
  <nav
    class="hidden tablet:block pt-[28px] pl-[38px] pr-[120px] border-t border-borderGray"
  >
    <ul class="flex justify-between text-xl font-semibold gap-[20px] uppercase">
      
      <li>
        <router-link
          class="transition-colors inline-block text-blue hover:text-lightYellow"
          :to="{ name: 'About' }"
          >{{ t('about') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue hover:text-lightYellow"
          :to="{ name: 'Genre' }"
          >{{ t('genre') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue  hover:text-lightYellow"
          :to="{ name: 'Event' }"
          >{{ t('event') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue  hover:text-lightYellow"
          :to="{ name: 'News' }"
          >{{ t('news') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue  hover:text-lightYellow"
          :to="{ name: 'Member' }"
          >{{ t('member') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue  hover:text-lightYellow"
          :to="{ name: 'Library' }"
          >{{ t('library') }}</router-link
        >
      </li>
      <li>
        <router-link
          class="transition-colors inline-block text-blue  hover:text-lightYellow"
          :to="{ name: 'Contact' }"
          >{{ t('contact') }}</router-link
        >
      </li>
    </ul>
  </nav>
</template>
<script setup>
import { useI18n } from 'vue-i18n';
const { t } = useI18n();
</script>
<style></style>
