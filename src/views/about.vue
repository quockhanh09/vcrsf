<template>
  <main>
    <NavAbout class="hidden tablet:block" />
    <router-view></router-view>
  </main>
</template>

<script setup>
import NavAbout from '@/components/pages/about/_nav-about.vue';
</script>
<style scoped></style>
