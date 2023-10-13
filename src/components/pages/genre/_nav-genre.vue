<template>
  <section>
    <nav
      class="tablet:bg-bgBlack tablet:text-white tablet:py-[20px] tablet:px-[240px]"
    >
      <ul
        class="tablet:h-[72px] flex flex-col tablet:flex-row justify-start tablet:justify-between tablet:items-center gap-[20px] tablet:gap-0 uppercase"
      >
        <li v-for="genre in genres" :key="genre.id">
          <router-link
            :to="{
              name: 'GenreDetails',
              params: { id: genre.name },
            }"
            @click="emit('handleShow')"
            >{{ genre.name }}</router-link
          >
        </li>
      </ul>
    </nav>
  </section>
</template>

<script setup>
import getGenres from '@/composables/getGenres';
import { onMounted } from 'vue';
const emit = defineEmits(['handleShow']);
const { genres, fetchDataGenres } = getGenres('');
onMounted(async () => {
  await fetchDataGenres();
});
</script>

<style scoped></style>
