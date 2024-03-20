<template>
  <div>
    <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
      <Chirp v-for="chirpT in chirps" :key="chirpT.id" :chirp="chirpT" />
    </div>
  </div>
</template>

<script setup>
const { $apiFetch } = useNuxtApp();

const chirps = await $apiFetch("/api/chirps");
</script>
