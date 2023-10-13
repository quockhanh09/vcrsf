<template>
  <div>
    <div class="my-16">
      <h2>{{ t('about') }}</h2>
    </div>
    <div class="text-xl">
      <p>
        {{ props.intro }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const props = defineProps(['intro']);
</script>
