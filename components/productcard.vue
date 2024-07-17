<script setup>
import { defineProps } from 'vue';

defineProps({
    image: String,
    title: String,
    description: String,
    price: Number
})
const truncateDescription = (text, length = 100) => {
    if (text.length <= length) {
        return text;
    }
    return text.slice(0, length) + '...';
};
const truncatetitle= (text, length = 12) => {
    if (text.length <= length) {
        return text;
    }
    return text.slice(0, length) + '...';
};
</script>

<template>
    <div class="p-2">  
        <div class="max-w-sm rounded overflow-hidden shadow-lg">
            <img class="w-full h-72" :src="image" :alt="title">
            <div class="px-6 py-4">
                <div class="font-bold text-xl mb-2">{{ truncatetitle(title) }}</div>
                <p class="text-gray-700 text-base">
                    {{ truncateDescription(description) }}
                </p>
            </div>
            <div class="px-6 pt-4 pb-2">
                <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">Price: ${{ price.toFixed(2) }}</span>
            </div>
        </div>
    </div>
</template>