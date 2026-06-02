<template>
  <div class="flex flex-col items-center justify-center py-20 px-4 text-center">
    <div class="w-24 h-24 mb-6 rounded-full bg-slate-100 flex items-center justify-center" data-ce='[{"k":"t-light-class","v":"bg-slate-100"},{"k":"t-dark-class","v":"bg-slate-800"}]'>
      <svg class="w-12 h-12 text-slate-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
    </div>
    <h3 class="text-xl font-semibold text-slate-900 mb-2" data-ce='[{"k":"t-light-class","v":"text-slate-900"},{"k":"t-dark-class","v":"text-white"}]'>{{ title }}</h3>
    <p class="text-slate-500 max-w-md mx-auto mb-8" data-ce='[{"k":"t-light-class","v":"text-slate-500"},{"k":"t-dark-class","v":"text-slate-400"}]'>{{ description }}</p>
    
    <button 
      v-if="showAction"
      @click="$emit('action')"
      class="inline-flex items-center justify-center px-6 py-3 border border-transparent text-sm font-medium rounded-lg text-indigo-700 bg-indigo-100 hover:bg-indigo-200 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 shadow-sm"
      data-ce='[{"k":"t-light-class","v":"text-indigo-700 bg-indigo-100 hover:bg-indigo-200"},{"k":"t-dark-class","v":"text-indigo-300 bg-indigo-900/50 hover:bg-indigo-800/60 focus:ring-offset-slate-900"}]'
    >
      {{ actionText }}
    </button>
  </div>
</template>

<script lang="ts" setup>
const props = defineProps({
  title: {
    type: String,
    default: 'No products found'
  },
  description: {
    type: String,
    default: 'Try adjusting your search or filters to find what you are looking for.'
  },
  showAction: {
    type: Boolean,
    default: true
  },
  actionText: {
    type: String,
    default: 'Clear all filters'
  }
});

defineEmits(['action']);
</script>
