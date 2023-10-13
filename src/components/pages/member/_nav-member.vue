<template>
  <section>
    <nav
      class="tablet:bg-bgBlack tablet:text-white tablet:py-[20px] tablet:px-[240px]"
    >
      <ul
        class="tablet:h-[72px] flex flex-col tablet:flex-row justify-start tablet:justify-end tablet:items-center gap-[20px] tablet:gap-[40px] uppercase"
      >
        <li>
          <router-link
            :to="{
              name: 'Personal',
            }"
            @click="emit('handleShow')"
            >{{ t('personal') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'Organization',
            }"
            @click="emit('handleShow')"
            >{{ t('organization') }}</router-link
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

<style scoped></style>
