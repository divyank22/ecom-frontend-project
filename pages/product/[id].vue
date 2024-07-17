<template>
  <div v-if="item" class="flex flex-col md:flex-row justify-center items-center p-4 max-w-4xl mx-auto">
    <img class="w-full md:w-1/2 h-auto object-cover mb-4 md:mb-0 md:mr-4" :src="item.image" :alt="item.title">
    <div class="md:w-1/2">
      <h1 class="text-2xl font-bold mb-2">{{ item.title }}</h1>
      <p class="text-gray-700 mb-4">{{ item.description }}</p>
      <p class="text-xl font-semibold">Price: ${{ item.price }}</p>
    </div>
  </div>
  <div v-else class="text-center py-8">
    Loading...
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const item = ref(null);

onMounted(async () => {
  const itemId = route.params.id;
  try {
    const response = await fetch(`https://fakestoreapi.com/products/${itemId}`);
    const data = await response.json();
    item.value = data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>