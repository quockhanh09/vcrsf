<template>
  <section>
    <nav
      class="tablet:bg-bgBlack tablet:text-white tablet:py-[20px] tablet:px-[240px]"
    >
      <ul
        class="tablet:h-[72px] flex flex-col tablet:flex-row justify-start tablet:justify-between tablet:items-center gap-[20px] tablet:gap-0 uppercase"
      >
        <li>
          <router-link
            :to="{
              name: 'LegalDocument',
            }"
            @click="emit('handleShow')"
            >{{ t('legal-doc') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'LawRegulations',
            }"
            @click="emit('handleShow')"
            >{{ t('law-regulations') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'References',
            }"
            @click="emit('handleShow')"
            >{{ t('references') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'PhotoGallery',
            }"
            @click="emit('handleShow')"
            >{{ t('photo') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'VideoGallery',
            }"
            @click="emit('handleShow')"
            >{{ t('video') }}</router-link
          >
        </li>
      </ul>
    </nav>
  </section>
</template>
<script setup>
import { useI18n } from 'vue-i18n';
const { t } = useI18n();
const emit = defineEmits(['handleShow']);
</script>

<style></style>
