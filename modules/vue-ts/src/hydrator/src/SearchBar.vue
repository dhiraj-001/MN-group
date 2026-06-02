<template>
  <div class="relative w-full">
    <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
      <svg class="h-5 w-5 text-slate-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
        <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
      </svg>
    </div>
    <input 
      type="text" 
      v-model="searchQuery"
      @input="handleInput"
      placeholder="Search products..." 
      class="block w-full pl-10 pr-10 py-2 border border-slate-200 rounded-lg leading-5 bg-white placeholder-slate-400 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm transition-colors shadow-sm"
      data-ce='[{"k":"t-light-class","v":"bg-white border-slate-200 text-slate-900 placeholder-slate-400 focus:ring-indigo-500 focus:border-indigo-500"},{"k":"t-dark-class","v":"bg-slate-800 border-slate-700 text-white placeholder-slate-500 focus:ring-indigo-400 focus:border-indigo-400"}]'
    >
    <button 
      v-if="searchQuery" 
      @click="clearSearch"
      class="absolute inset-y-0 right-0 pr-3 flex items-center text-slate-400 hover:text-slate-600 transition-colors"
      data-ce='[{"k":"t-light-class","v":"text-slate-400 hover:text-slate-600"},{"k":"t-dark-class","v":"text-slate-500 hover:text-slate-300"}]'
    >
      <svg class="h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
      </svg>
    </button>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const emit = defineEmits(['search', 'clear']);

const searchQuery = ref('');

const handleInput = () => {
  emit('search', searchQuery.value);
};

const clearSearch = () => {
  searchQuery.value = '';
  emit('clear');
  emit('search', '');
};
</script>
