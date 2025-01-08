<template>
  <header>
    <nav class="flex w-auto bg-blue-600 mx-1 justify-between shadow-2xl rounded-md">
      <h1 class="text-5xl my-auto">ecom</h1>
      <ul class="flex list-none">
        <nuxt-link to="/" class="mx-1 md:mx-4 my-auto hover:text-gray-200 transition-colors duration-200">Home</nuxt-link>
        <nuxt-link to="/product" class="mx-1 md:mx-4 my-auto hover:text-gray-200 transition-colors duration-200">Products</nuxt-link>
        <nuxt-link to="/about" class="mx-1 md:mx-4 my-auto hover:text-gray-200 transition-colors duration-200">About</nuxt-link>
        <div id="search-toggle" @click="search_toggle" class="search-icon cursor-pointer pl-6 mx-1 md:mx-4 my-auto" aria-label="Toggle search">
          <svg class="fill-current pointer-events-none text-grey-darkest w-4 h-4 inline" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
            <path d="M12.9 14.32a8 8 0 1 1 1.41-1.41l5.35 5.33-1.42 1.42-5.33-5.34zM8 14A6 6 0 1 0 8 2a6 6 0 0 0 0 12z"></path>
          </svg>
        </div>
      </ul>
    </nav>
    
    <div ref="searchContent" class="relative w-full hidden bg-white shadow-xl" id="search-content">
      <div class="container mx-auto py-4 text-black">
        <input ref="searchField" v-model="searchTerm" type="search" placeholder="Search..." autofocus class="w-full text-grey-800 transition focus:outline-none focus:border-transparent p-2 appearance-none leading-normal text-xl lg:text-2xl">
      </div>
      <div class="grid grid-cols-2 md:grid-cols-4">
        <div v-for="item in filteredItems" :key="item.id">
          <nuxt-link @click="search_toggle" :to="'/product/' + item.id">
            <productcard :image="item.image" :title="item.title" :description="item.description" :price="item.price"/>
          </nuxt-link>
        </div>
      </div>
    </div>
    <div v-if="filteredItems.length === 0" class="text-center mt-4">
      No products found matching your search.
    </div>
  </header>
  <div>
    <slot></slot>
  </div>
</template>

  <script setup>
  import { ref, onMounted, computed } from 'vue';
  
  const items = ref([]);
  const searchContent = ref(null);
  const searchField = ref(null);
  const searchTerm = ref('');
  
  // Fetching data from an API
  onMounted(async () => {
    try {
      const response = await fetch("https://fakestoreapi.com/products");
      const data = await response.json();
      items.value = data;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  });
  
  // Computed property for filtering items
  const filteredItems = computed(() => {
    if (!searchTerm.value) return items.value;
    return items.value.filter(item => 
      item.title.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      item.description.toLowerCase().includes(searchTerm.value.toLowerCase())
    );
  });
  
  // Search toggle function to show/hide search bar
  function search_toggle() {
    searchContent.value.classList.toggle('hidden');
    if (!searchContent.value.classList.contains('hidden')) {
      searchField.value.focus(); // Focus the search input when the search bar is shown
    }
  }
  </script>