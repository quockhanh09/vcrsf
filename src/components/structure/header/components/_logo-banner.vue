<template>
  <section
    class="h-full tablet:py-[24px] tablet:pl-[120px] tablet:pr-[75.75px] border-0 tablet:border-l-0 tablet:border-r border-borderGray"
  >
    <img
      class="h-[100px] tablet:h-[150px] cursor-pointer object-cover tablet:object-contain"
      src="@/assets/images/vcrsf_logo.svg"
      alt="vcrsf logo"
      @click="() => router.push({ name: 'Home' })"
    />
  </section>
</template>
<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();
</script>

<style></style>
