<!-- src/components/ApiComponent.vue -->
<template>
  <div
    class="max-w-md mx-auto mt-8 p-6 bg-gray-100 rounded-lg shadow-md text-center"
  >
    <button
      @click="fetchData"
      :class="{ 'opacity-50 cursor-not-allowed': isLoading }"
      class="bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-600 mb-4"
    >
      {{ isLoading ? "Fetching..." : "Fetch Data" }}
    </button>
    <div v-if="error" class="text-red-500 mb-4">
      <p>Error: {{ error }}</p>
    </div>
    <div v-if="isLoading" class="mt-4">
      <div
        class="animate-spin inline-block h-6 w-6 border-t-2 border-blue-500"
      ></div>
      <span class="ml-2 text-blue-500">Loading...</span>
    </div>
    <div v-if="quote" class="text-left">
      <p class="text-lg font-bold mb-2">Quote:</p>
      <p class="text-gray-700">{{ quote }}</p>
      <p class="text-lg font-bold mt-4 mb-2">Anime:</p>
      <p class="text-gray-700">{{ anime }}</p>
      <p class="text-lg font-bold mt-4 mb-2">Character:</p>
      <p class="text-gray-700">{{ character }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const quote = ref(null);
const anime = ref(null);
const character = ref(null);
const isLoading = ref(false);
const error = ref(null);

const fetchData = async () => {
  try {
    isLoading.value = true;
    const response = await fetch("https://animechan.xyz/api/random");

    if (!response.ok) {
      throw new Error(`Failed to fetch data. Status: ${response.status}`);
    }

    const data = await response.json();

    quote.value = data.quote;
    anime.value = data.anime;
    character.value = data.character;
    error.value = null;
  } catch (err) {
    console.error("Error fetching data:", err.message);
    error.value = "Failed to fetch data. Please try again later.";
  } finally {
    isLoading.value = false;
  }
};
</script>

<style scoped>
/* Add any custom styles here */
</style>
