<template>
  <span 
    class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold tracking-wider transition-colors border"
    :class="baseClasses"
    :data-ce="dataCeConfig"
  >
    {{ label }}
    
    <!-- Optional Remove 'X' Icon -->
    <button 
      v-if="removable" 
      @click.stop="emit('remove')"
      class="ml-2 -mr-1 flex-shrink-0 h-4 w-4 rounded-full inline-flex items-center justify-center focus:outline-none transition-colors"
      :class="closeButtonClasses"
    >
      <span class="sr-only">Remove {{ label }}</span>
      <svg class="h-2.5 w-2.5" stroke="currentColor" fill="none" viewBox="0 0 8 8">
        <path stroke-linecap="round" stroke-width="1.5" d="M1 1l6 6m0-6L1 7" />
      </svg>
    </button>
  </span>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import type { _p_TYP, _pp_TYP } from "../../shared/types";

const props = withDefaults(defineProps<{
    _p?: _p_TYP,
    _pp?: _pp_TYP,
    label: string,
    variant?: 'primary' | 'success' | 'warning' | 'danger' | 'neutral',
    removable?: boolean
}>(), {
    variant: 'neutral',
    removable: false
});

const emit = defineEmits(['remove']);

// Base classes for the pill shape
const baseClasses = computed(() => {
    switch (props.variant) {
        case 'primary': return 'bg-indigo-50 border-indigo-200 text-indigo-700';
        case 'success': return 'bg-emerald-50 border-emerald-200 text-emerald-700';
        case 'warning': return 'bg-amber-50 border-amber-200 text-amber-700';
        case 'danger':  return 'bg-rose-50 border-rose-200 text-rose-700';
        case 'neutral': 
        default:        return 'bg-slate-100 border-slate-200 text-slate-700';
    }
});

// Specific hover classes for the remove 'X' button
const closeButtonClasses = computed(() => {
    switch (props.variant) {
        case 'primary': return 'text-indigo-400 hover:bg-indigo-200 hover:text-indigo-600 focus:bg-indigo-500 focus:text-white';
        case 'success': return 'text-emerald-400 hover:bg-emerald-200 hover:text-emerald-600 focus:bg-emerald-500 focus:text-white';
        case 'warning': return 'text-amber-400 hover:bg-amber-200 hover:text-amber-600 focus:bg-amber-500 focus:text-white';
        case 'danger':  return 'text-rose-400 hover:bg-rose-200 hover:text-rose-600 focus:bg-rose-500 focus:text-white';
        case 'neutral': 
        default:        return 'text-slate-400 hover:bg-slate-200 hover:text-slate-600 focus:bg-slate-500 focus:text-white';
    }
});

// Dynamic data-ce config for dark mode support based on variant
const dataCeConfig = computed(() => {
    let darkClass = '';
    switch (props.variant) {
        case 'primary': darkClass = 'bg-indigo-900/40 border-indigo-700 text-indigo-300'; break;
        case 'success': darkClass = 'bg-emerald-900/40 border-emerald-700 text-emerald-300'; break;
        case 'warning': darkClass = 'bg-amber-900/40 border-amber-700 text-amber-300'; break;
        case 'danger':  darkClass = 'bg-rose-900/40 border-rose-700 text-rose-300'; break;
        case 'neutral': 
        default:        darkClass = 'bg-slate-800 border-slate-700 text-slate-300'; break;
    }
    
    return JSON.stringify([
        {"k":"t-light-class", "v": baseClasses.value},
        {"k":"t-dark-class", "v": darkClass}
    ]);
});
</script>
