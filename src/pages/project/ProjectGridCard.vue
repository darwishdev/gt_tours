<template>
  <Motion
    :initial="{ opacity: 0, y: 30 }"
    :while-in-view="{ opacity: 1, y: 0 }"
    :transition="{ delay: 0.1 * index, duration: 0.6, ease: 'easeOut' }"
  >
    <div
      class="group relative transform rounded-3xl bg-[#F5F5F7] p-8 md:p-12 transition duration-300 hover:-translate-y-2 hover:shadow-2xl dark:bg-neutral-800"
    >
      <!-- Title and Location -->
      <div class="text-center transition-colors duration-300">
        <h3
          class="mb-1 text-xl font-bold text-neutral-800 dark:text-white group-hover:text-green-700"
        >
          {{ title }}
        </h3>
        <p
          class="text-xs uppercase tracking-wide text-green-600 mb-4 group-hover:tracking-wider transition-all"
        >
          📍 {{ location }}
        </p>
        <p
          class="text-base text-neutral-600 dark:text-neutral-300 transition duration-300 group-hover:text-neutral-800 dark:group-hover:text-white"
        >
          {{ description }}
        </p>
      </div>

      <!-- Image with Category Overlay -->
      <div
        class="relative mx-auto mt-8 w-full max-w-md overflow-hidden rounded-xl"
      >
        <img
          :src="src"
          :alt="title"
          class="h-64 w-full rounded-xl object-cover transition-transform duration-500 group-hover:scale-105"
        />
        <div
          class="absolute bottom-0 left-0 w-full bg-gradient-to-t from-black/30 to-transparent px-4 py-2 text-left text-xs font-medium text-white"
        >
          {{ category }}
        </div>
      </div>
    </div>
  </Motion>
</template>

<script setup lang="ts">
import { Motion } from "motion-v";

defineProps<{
  title: string;
  description: string;
  location: string;
  category: string;
  src: string;
  index: number;
}>();
</script>
