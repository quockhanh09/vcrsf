<template>
  <section
    class="bg-black w-full h-[80px] tablet:h-[250px] tablet:py-[16px] flex justify-between items-stretch"
  >
    <div
      class="count-down title relative w-1/2 h-[60px] tablet:h-[178px] m-auto"
    >
      <div class="container tablet:pl-[120px] tablet:pr-[55px]">
        <h3 class="mt-[4px] tablet:mt-[16px] text-[10px] tablet:text-[32px]">
          {{ events[0]?.fields.name }}
        </h3>
        <div
          class="absolute right-[10px] tablet:right-[50px] bottom-[5px] tablet:bottom-[25px] flex justify-end"
        >
          <button
            class="w-[51px] h-[16px] tablet:w-[120px] tablet:h-[40px] tablet:p-2 bg-yellow text-[6px] tablet:text-base font-medium rounded-[30px]"
          >
            {{ t('view-detail') }}
          </button>
        </div>
      </div>
    </div>
    <div
      class="container w-1/2 py-[4px] tablet:py-auto tablet:pl-16 text-yellow"
    >
      <div class="flex">
        <img
          class="mr-[4px] tablet:mr-[12px] w-[10px] h-[10px] tablet:w-[24px] tablet:h-[24px]"
          src="@/assets/images/home-page/countdown.svg"
          alt="countdown svg"
        />
        <p class="text-[8px] tablet:text-xl font-medium">
          {{ t('time-remain') }}
        </p>
      </div>
      <div
        class="tablet:mt-4 flex text-[8px] tablet:text-base justify-start tablet:gap-[100px]"
      >
        <h5 class="">{{ t('day') }}</h5>
        <h5 class="mx-[20px]">{{ t('hours') }}</h5>
        <h5 class="mx-[5px] tablet:mx-0">{{ t('minutes') }}</h5>
        <h5 class="mx-[20px]">{{ t('seconds') }}</h5>
      </div>
      <div class="font-medium">
        <p
          class="text-[24px] tablet:text-6xl tracking-[2px] tablet:tracking-[16px]"
        >
          {{ countdown }}
        </p>
        <p class="text-[8px] tablet:text-2xl">{{ formattedCountdown }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useI18n } from 'vue-i18n';
import { formatDate, formatNumber } from '@/plugins/date-utils.js';
import getEvents from '@/composables/getEvents.js';
const { t } = useI18n();
const targetDate = ref(null);
const countdown = ref('');
const formattedCountdown = ref('');
const { events, fetchDataEvents } = getEvents('');

const updateCountdown = () => {
  const now = new Date();
  const eventDate = events.value[0]?.fields.dates;
  if (!eventDate || new Date(eventDate) - now < 0) {
    countdown.value = '00 00:00:00';
  } else {
    const diff = new Date(eventDate) - now;
    const days = Math.floor(diff / (1000 * 60 * 60 * 24));
    const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
    const seconds = Math.floor((diff % (1000 * 60)) / 1000);
    countdown.value = `${formatNumber(days, 2)} ${formatNumber(
      hours,
      2
    )}:${formatNumber(minutes, 2)}:${formatNumber(seconds, 2)}`;
    formattedCountdown.value = formatDate(eventDate);
  }
};
setInterval(updateCountdown, 1000);
onMounted(async () => {
  await fetchDataEvents();
  const date = events.value[0]?.times;
  targetDate.value = new Date(date);
  updateCountdown(); // Call the function once to initialize the countdown
});
</script>

<style scoped>
.count-down.title {
  background-color: rgba(249, 247, 240, 1);
  fill: #f9f7f0;
}
</style>
