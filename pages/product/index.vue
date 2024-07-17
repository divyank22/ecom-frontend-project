<script setup>
import { ref, onMounted } from 'vue';
const items = ref([]);
onMounted(async () => {
  try {
    const response = await fetch("https://fakestoreapi.com/products");
    const data = await response.json();
    items.value = data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});
</script>


<template>
  <div class="grid grid-cols-2 sm:grid-cols-4">
    <div v-for="item in items" :key="item.id">
      <nuxt-link :to="'/product/' + item.id">
        <productcard :image="item.image" :title="item.title" :description="item.description" :price="item.price" />
      </nuxt-link>
    </div>
  </div>
</template>
