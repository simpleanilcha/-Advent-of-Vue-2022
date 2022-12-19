<script setup>
import { ref, watch } from 'vue'

const searchTerm = ref('')
const products = ref([])
const isLoading = ref(false)
const hasNoResults = ref(false)

// debounce method from https://levelup.gitconnected.com/debounce-in-javascript-improve-your-applications-performance-5b01855e086

const debounce = (func, wait) => {
  let timeout;

  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };

    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
};

const findProducts = async term => {
  if (term.length) {
    const response = await fetch(`https://dummyjson.com/products/search?q=${term}&limit=10`)
    const data = await response.json()
    products.value = data.products
    isLoading.value = false
    hasNoResults.value = !products.value.length
  } else {
    isLoading.value = false
    products.value = []
  }
}

watch(searchTerm, () => {
  isLoading.value = true
})
watch(searchTerm, debounce(findProducts, 300))

</script>

<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input type="text" class="p-2 border-2 border-gray-dark" v-model="searchTerm" placeholder="Start typing..." />
    <p v-if="hasNoResults && !isLoading">No results found.</p>
    <p v-if="isLoading">Loading...</p>
    <ul class="list-disc" v-else>
      <li v-for="product in products" :key="product.id">
        {{ product.title }} - ${{ product.price }}
      </li>
    </ul>
  </div>
</template>
