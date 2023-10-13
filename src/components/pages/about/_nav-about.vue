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
              name: 'AboutDetails',
              params: { id: 'Giới thiệu' },
            }"
            @click="emit('handleShow')"
            >{{ t('federations') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'AboutDetails',
              params: { id: 'Tầm nhìn' },
            }"
            @click="emit('handleShow')"
            >{{ t('evolutions') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'AboutDetails',
              params: { id: 'Sứ mệnh' },
            }"
            @click="emit('handleShow')"
            >{{ t('missions') }}</router-link
          >
        </li>
        <li>
          <router-link
            :to="{
              name: 'AboutDetails',
              params: { id: 'Sơ đồ tổ chức' },
            }"
            @click="emit('handleShow')"
            >{{ t('diagrams') }}</router-link
          >
        </li>
      </ul>
    </nav>
  </section>
</template>
<script setup>
import { useI18n } from 'vue-i18n';
const emit = defineEmits(['handleShow']);
const { t } = useI18n();
</script>

<style scoped></style>
