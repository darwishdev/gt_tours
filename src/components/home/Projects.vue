<template>
  <section class="bg-white py-24 text-gray-900 dark:bg-black dark:text-white">
    <div class="max-w-7xl mx-auto px-6 text-center mb-16">
      <Motion
        :initial="{ opacity: 0, y: 40 }"
        :while-in-view="{ opacity: 1, y: 0 }"
        :transition="{ duration: 0.6, ease: 'easeOut' }"
      >
        <h2 class="text-4xl font-bold mb-4">{{ title }}</h2>
        <p class="max-w-2xl mx-auto text-gray-600 dark:text-gray-300">
          {{ description }}
        </p>
      </Motion>
    </div>

    <AppleCardCarousel>
      <AppleCarouselItem
        v-for="(card, index) in items"
        :key="index"
        :index="index"
      >
        <AppleCard :card="card" :index="index" :layout="true">
          <Motion
            :initial="{ opacity: 0, y: 30 }"
            :while-in-view="{ opacity: 1, y: 0 }"
            :transition="{ delay: 0.1 * index, duration: 0.5, ease: 'easeOut' }"
          >
            <div
              class="group relative mb-4 transform rounded-3xl bg-[#F5F5F7] p-8 md:p-14 transition duration-300 hover:-translate-y-2 hover:shadow-2xl dark:bg-neutral-800"
            >
              <div
                v-if="card.title || card.location || card.description"
                class="text-center transition-colors duration-300 mb-8"
              >
                <h3
                  v-if="card.title"
                  class="mb-1 text-xl font-bold text-neutral-800 dark:text-white group-hover:text-green-700"
                >
                  {{ card.title }}
                </h3>
                <p
                  v-if="card.location"
                  class="text-xs uppercase tracking-wide text-green-600 mb-4 group-hover:tracking-wider transition-all"
                >
                  📍 {{ card.location }}
                </p>
                <p
                  v-if="card.description"
                  class="text-base text-neutral-600 dark:text-neutral-300 transition duration-300 group-hover:text-neutral-800 dark:group-hover:text-white"
                >
                  {{ card.description }}
                </p>
              </div>

              <div
                class="relative mx-auto w-full max-w-md overflow-hidden rounded-xl"
              >
                <img
                  :src="card.src"
                  :alt="card.title || 'card image'"
                  class="h-64 w-full rounded-xl object-cover transition-transform duration-500 group-hover:scale-105"
                />
                <div
                  v-if="card.category"
                  class="absolute bottom-0 left-0 w-full bg-gradient-to-t from-black/30 to-transparent px-4 py-2 text-left text-xs font-medium text-white"
                >
                  {{ card.category }}
                </div>
              </div>
            </div>
          </Motion>
        </AppleCard>
      </AppleCarouselItem>
    </AppleCardCarousel>
  </section>
</template>

<script setup lang="ts">
import { Motion } from "motion-v";
import AppleCardCarousel from "@/components/ui/apple-card-carousel/AppleCardCarousel.vue";
import AppleCarouselItem from "@/components/ui/apple-card-carousel/AppleCarouselItem.vue";
import AppleCard from "@/components/ui/apple-card-carousel/AppleCard.vue";

defineProps<{
  title?: string;
  description?: string;
  items: {
    title?: string;
    description?: string;
    location?: string;
    category?: string;
    src: string;
  }[];
}>();
</script>
