<!-- components/EgyptDottedMap.vue -->
<script setup lang="ts">
import { ref, onMounted } from "vue";
import DottedMap from "dotted-map";

const svg = ref("");

onMounted(async () => {
  const map = new DottedMap({
    height: 32,
    grid: "diagonal",
    region: {
      // Egypt bounds
      lat: { min: 21.5, max: 32.8 },
      lng: { min: 24.5, max: 36.5 },
    },
  });

  const egyptCities = [
    // North Coast
    { lat: 31.2001, lng: 29.9187 }, // Alexandria
    { lat: 31.0364, lng: 31.3807 }, // Mansoura
    { lat: 30.5965, lng: 32.2715 }, // Ismailia
    { lat: 31.2653, lng: 32.3019 }, // Port Said

    // Greater Cairo
    { lat: 30.0444, lng: 31.2357 }, // Cairo
    { lat: 29.9870, lng: 31.2118 }, // Giza
    { lat: 30.0131, lng: 31.2089 }, // Dokki
    { lat: 30.0626, lng: 31.2497 }, // Downtown Cairo

    // Delta / Canal
    { lat: 30.7872, lng: 30.9995 }, // Zagazig
    { lat: 30.5549, lng: 31.0124 }, // Benha
    { lat: 30.5833, lng: 31.5167 }, // 10th of Ramadan

    // Upper Egypt
    { lat: 27.1809, lng: 31.1837 }, // Assiut
    { lat: 26.1551, lng: 32.7160 }, // Sohag
    { lat: 25.6872, lng: 32.6396 }, // Qena
    { lat: 25.6872, lng: 32.6396 }, // Luxor
    { lat: 24.0889, lng: 32.8998 }, // Aswan

    // Red Sea
    { lat: 27.2579, lng: 33.8116 }, // Hurghada
    { lat: 25.0676, lng: 34.8789 }, // Marsa Alam
    { lat: 28.3774, lng: 34.4666 }, // El Gouna area

    // Sinai
    { lat: 27.9158, lng: 34.3299 }, // Sharm El-Sheikh
    { lat: 28.5091, lng: 34.5136 }, // Dahab
    { lat: 29.3100, lng: 34.2400 }, // Nuweiba
    { lat: 28.5558, lng: 33.9750 }, // St. Catherine

    // Western Desert / Oases
    { lat: 29.2050, lng: 25.5197 }, // Siwa
    { lat: 25.4510, lng: 30.5460 }, // Kharga
  ];

  egyptCities.forEach((city) =>
    map.addPin({
      ...city,
      svgOptions: { color: "darkgreen", radius: 0.1 },
    }),
  );

  svg.value = map.getSVG({
    radius: 0.09,
    backgroundColor: "transparent",
    color: "#00000040",
    shape: "circle",
  });
});
</script>

<template>
  <div class="flex justify-center items-center p-4">
    <div class="w-full max-w-4xl object-contain" v-html="svg" />
  </div>
</template>

<style scoped>
div > svg {
  width: 100%;
  height: auto;
  animation: fadein 0.5s ease-in-out;
}

@keyframes fadein {
  from {
    opacity: 0;
    transform: scale(0.98);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
