<template>
  <div class="space-y-8">
    <!-- Categories -->
    <div>
      <h3 class="text-sm font-semibold text-slate-900 uppercase tracking-wider mb-4" data-ce='[{"k":"t-light-class","v":"text-slate-900"},{"k":"t-dark-class","v":"text-slate-300"}]'>Categories</h3>
      <div class="space-y-3">
        <label v-for="category in categories" :key="category" class="flex items-center space-x-3 cursor-pointer group">
          <div class="relative flex items-center justify-center">
            <input type="checkbox" class="peer appearance-none h-5 w-5 border-2 border-slate-300 rounded checked:bg-indigo-600 checked:border-transparent focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 transition-all duration-200" data-ce='[{"k":"t-light-class","v":"border-slate-300"},{"k":"t-dark-class","v":"border-slate-600 focus:ring-offset-slate-900"}]'>
            <svg class="absolute w-3 h-3 text-white pointer-events-none opacity-0 peer-checked:opacity-100 transition-opacity duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <span class="text-slate-700 group-hover:text-indigo-600 font-medium transition-colors" data-ce='[{"k":"t-light-class","v":"text-slate-700 group-hover:text-indigo-600"},{"k":"t-dark-class","v":"text-slate-300 group-hover:text-indigo-400"}]'>{{ category }}</span>
        </label>
      </div>
    </div>

    <hr class="border-slate-200" data-ce='[{"k":"t-light-class","v":"border-slate-200"},{"k":"t-dark-class","v":"border-slate-700"}]' />

    <!-- Price Range -->
    <div>
      <h3 class="text-sm font-semibold text-slate-900 uppercase tracking-wider mb-4" data-ce='[{"k":"t-light-class","v":"text-slate-900"},{"k":"t-dark-class","v":"text-slate-300"}]'>Price Range</h3>
      <div class="flex items-center space-x-4">
        <div class="flex-1">
          <label class="sr-only">Min Price</label>
          <div class="relative rounded-md shadow-sm">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <span class="text-slate-500 sm:text-sm">$</span>
            </div>
            <input type="number" placeholder="Min" class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-7 pr-3 py-2.5 sm:text-sm border-slate-300 rounded-lg bg-slate-50 border outline-none transition-shadow" data-ce='[{"k":"t-light-class","v":"bg-slate-50 border-slate-300 text-slate-900"},{"k":"t-dark-class","v":"bg-slate-800 border-slate-600 text-white"}]'>
          </div>
        </div>
        <span class="text-slate-400">-</span>
        <div class="flex-1">
          <label class="sr-only">Max Price</label>
          <div class="relative rounded-md shadow-sm">
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <span class="text-slate-500 sm:text-sm">$</span>
            </div>
            <input type="number" placeholder="Max" class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-7 pr-3 py-2.5 sm:text-sm border-slate-300 rounded-lg bg-slate-50 border outline-none transition-shadow" data-ce='[{"k":"t-light-class","v":"bg-slate-50 border-slate-300 text-slate-900"},{"k":"t-dark-class","v":"bg-slate-800 border-slate-600 text-white"}]'>
          </div>
        </div>
      </div>
    </div>

    <hr class="border-slate-200" data-ce='[{"k":"t-light-class","v":"border-slate-200"},{"k":"t-dark-class","v":"border-slate-700"}]' />

    <!-- Availability -->
    <div>
      <h3 class="text-sm font-semibold text-slate-900 uppercase tracking-wider mb-4" data-ce='[{"k":"t-light-class","v":"text-slate-900"},{"k":"t-dark-class","v":"text-slate-300"}]'>Availability</h3>
      <div class="space-y-3">
        <label class="flex items-center space-x-3 cursor-pointer group">
          <div class="relative flex items-center justify-center">
            <input type="checkbox" checked class="peer appearance-none h-5 w-5 border-2 border-slate-300 rounded checked:bg-indigo-600 checked:border-transparent focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 transition-all duration-200" data-ce='[{"k":"t-light-class","v":"border-slate-300"},{"k":"t-dark-class","v":"border-slate-600 focus:ring-offset-slate-900"}]'>
            <svg class="absolute w-3 h-3 text-white pointer-events-none opacity-0 peer-checked:opacity-100 transition-opacity duration-200" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="3">
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <span class="text-slate-700 group-hover:text-indigo-600 font-medium transition-colors" data-ce='[{"k":"t-light-class","v":"text-slate-700 group-hover:text-indigo-600"},{"k":"t-dark-class","v":"text-slate-300 group-hover:text-indigo-400"}]'>In Stock Only</span>
        </label>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const categories = ['Electronics', 'Accessories', 'Wearables', 'Audio', 'Computers', 'Gaming'];
</script>
