<template>
  <main>
    <section v-if="!loadingEvent">
      <div
        class="relative h-[100px] tablet:h-[300px] flex justify-center items-center"
      >
        <div class="absolute w-full h-full -z-20">
          <img class="w-full h-full" :src="defaultImg" alt="df img" />
        </div>
        <div class="">
          <h3 class="container text-yellow uppercase">
            {{ t('upcoming-events') }}
          </h3>
        </div>
      </div>
      <CountDownModal :event="eventDetails" />
      <div class="container py-16">
        <div
          class="border-t border-borderGray flex flex-col tablet:flex-row justify-between items-stretch"
        >
          <div class="tablet:w-2/3 pt-4 pr-8">
            <h5 class="text-[12px] tablet:text-2xl text-yellow font-bold">
              {{ eventDetails[0]?.fields.name }}
            </h5>
            <p class="my-8 text-[8px] tablet:text-xl break-words">
              {{ eventDetails[0]?.fields.intro }}
            </p>
          </div>
          <div
            class="tablet:w-1/3 border-t border-b tablet:border-t-0 tablet:border-b-0 tablet:border-l border-borderGray"
          >
            <div>
              <div class="p-4 flex flex-col gap-[10px]">
                <h6 class="text-[12px] tablet:text-xl font-bold">
                  Ngày diễn ra sự kiện
                </h6>
                <p class="text-[8px] tablet:text-base">
                  {{ formatDate(eventDetails[0]?.fields.dates) }}
                </p>
                <p class="text-[8px] tablet:text-base text-red">
                  {{ eventDetails[0]?.fields.status }}
                </p>
              </div>
            </div>
            <div class="border-y border-borderGray">
              <div class="p-4 flex flex-col gap-[20px]">
                <h6 class="text-[12px] tablet:text-xl font-bold">Vị trí</h6>
                <p class="text-[8px] tablet:text-base">
                  {{ eventDetails[0]?.fields.address }}
                </p>
              </div>
            </div>
            <div>
              <div class="py-8">
                <img class="m-auto" v-lazy="vcrsfLogo" alt="vcrsf logo" />
              </div>
              <div class="px-4 flex flex-col gap-[10px] tablet:gap-[20px]">
                <div class="flex justify-start items-center gap-[20px]">
                  <img
                    class="w-[12px] h-[12px] tablet:w-[24px] tablet:h-[24px]"
                    v-lazy="homeLogo"
                    alt="home logo"
                  />
                  <p class="text-[8px] tablet:text-base">
                    36 Trần Phú, Hà Nội, Việt Nam
                  </p>
                </div>
                <div class="flex justify-start items-center gap-[20px]">
                  <img
                    class="w-[12px] h-[12px] tablet:w-[24px] tablet:h-[24px]"
                    v-lazy="phoneLogo"
                    alt="phone logo"
                  />
                  <p class="text-[8px] tablet:text-base">(84) 4 - 3 7475908</p>
                </div>
                <div class="flex justify-start items-center gap-[20px]">
                  <img
                    class="w-[12px] h-[12px] tablet:w-[24px] tablet:h-[24px]"
                    v-lazy="emailLogo"
                    alt="email logo"
                  />
                  <p class="text-[8px] tablet:text-base">vcrsf@vnn.vn</p>
                </div>
                <div class="flex justify-start items-center gap-[20px]">
                  <img
                    class="w-[12px] h-[12px] tablet:w-[24px] tablet:h-[24px]"
                    v-lazy="webIc"
                    alt="web logo"
                  />
                  <p class="text-[8px] tablet:text-base">
                    Liên Đoàn Đua thuyền Việt Nam
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section v-else>
      <LoadingComponents />
    </section>
  </main>
</template>

<script setup>
import { useRoute } from 'vue-router';
import { onMounted, ref } from 'vue';
import { useI18n } from 'vue-i18n';
import defaultImg from '@/assets/images/default.png';
import vcrsfLogo from '@/assets/images/vcrsf_logo.svg';
import homeLogo from '@/assets/images/contact/home.png';
import phoneLogo from '@/assets/images/contact/baseline-phone.png';
import emailLogo from '@/assets/images/contact/email.png';
import webIc from '@/assets/images/web-ic.svg';
import CountDownModal from '@/modal/count-down-modal.vue';
import getEventDetails from '@/composables/getEventDetails.js';
import LoadingComponents from '../structure/loading-components/loading-components.vue';
import { formatDate } from '@/plugins/date-utils.js';
const { t } = useI18n();
const route = useRoute();
const eventId = ref(route.params.id);
const { eventDetails, loadingEvent, fetchDataEventDetails } = getEventDetails(
  eventId.value
);
onMounted(async () => await fetchDataEventDetails());
</script>

<style></style>
