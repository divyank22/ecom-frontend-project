<script setup>
import { ref, onMounted } from 'vue';
import  productcard  from '../components/productcard.vue';

const items = ref([]);

onMounted(async () => {
  try {
    const response = await fetch("https://fakestoreapi.com/products");
    const data = await response.json();
    items.value = data.slice(0, 5);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});

</script>

<template>
  <div class="mx-auto flex flex-col justify-center items-center h-96">
    <h1 class="text-center text-2xl font-bold mb-4">Welcome to Ecom</h1>
  </div>
  <div class="grid grid-cols-5">
      <div v-for="item in items" :key="item.id">
        <productcard :image="item.image" :title="item.title" :description="item.description" :price="item.price"/>
      </div>
    </div> 
</template>
