<template>
  <main>
    <section v-if="!loadingVideos">
      <div v-if="video" class="video-modal">
        <div class="header-video-modal">
          <div class="container flex items-center gap-[10px] tablet:gap-[40px]">
            <div
              class="cursor-pointer"
              @click="router.push({ name: 'VideoGallery' })"
            >
              <img v-lazy="arrowLeftIc" alt="arrow left ic" />
            </div>
            <div>
              <div>
                <h4 class="text-base tablet:text-3xl font-bold">
                  {{ video?.name }}
                </h4>
              </div>
              <div
                class="flex justify-start items-center gap-[40px] tablet:gap-[80px]"
              >
                <p class="text-[14px] tablet:text-base">
                  {{ formatDay(video?.created) }}
                </p>
                <p
                  class="genre-tag-video text-[12px] tablet:text-base text-yellow uppercase"
                >
                  {{ video?.category }}
                </p>
              </div>
            </div>
            <div class="ml-auto flex items-center gap-[10px]">
              <div>
                <p class="font-bold">Chia sẻ</p>
              </div>
              <div>
                <span class="font-bold">:</span>
              </div>
              <div>
                <ShareNetwork
                  network="facebook"
                  :url="shareUrl"
                  hashtags="liendoanduathuyenvietnam,duathuyen"
                >
                  <img v-lazy="fbIc" alt="facebook icon" />
                </ShareNetwork>
              </div>
            </div>
          </div>
        </div>
        <div class="container relative main-video-modal">
          <video controls :src="video?.video"></video>
        </div>
      </div>
      <div v-else>
        <NotFound />
      </div>
    </section>
    <section v-else>
      <LoadingComponents />
    </section>
  </main>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import { formatDay } from '@/plugins/date-utils.js';
import arrowLeftIc from '@/assets/images/library/arrow-left.svg';
import fbIc from '@/assets/images/fb-ic.svg';
import LoadingComponents from '@/components/structure/loading-components/loading-components.vue';
import NotFound from '@/components/structure/not-found-page/_not-found.vue';
import getVideoDetails from '@/composables/getVideoDetails.js';
const router = useRouter();
const route = useRoute();
const videoId = ref(route.params.id);
const shareUrl = ref(window.location.href);
const { video, loadingVideos, fetchDataVideoDetails } = getVideoDetails(
  videoId.value
);
onMounted(async () => await fetchDataVideoDetails());
</script>

<style scoped></style>
