<template>
  <Teleport to="body">
    <Transition name="fade">
      <!-- Overlay -->
      <div 
        v-if="isOpen" 
        class="fixed inset-0 z-40 bg-black/40 backdrop-blur-sm transition-opacity"
        @click="closeDrawer"
      ></div>
    </Transition>

    <Transition name="slide">
      <!-- Drawer Panel -->
      <div 
        v-if="isOpen" 
        class="fixed inset-y-0 right-0 z-50 w-full max-w-md shadow-2xl flex flex-col transform transition-transform duration-300 ease-in-out"
        data-ce='[{"k":"t-light-class","v":"bg-white text-slate-900"},{"k":"t-dark-class","v":"bg-slate-900 text-white"}]'
        :class="['bg-white text-slate-900']"
      >
        <!-- Header -->
        <div class="flex items-center justify-between p-6 border-b"
             data-ce='[{"k":"t-light-class","v":"border-slate-200"},{"k":"t-dark-class","v":"border-slate-800"}]'
             :class="['border-slate-200']"
        >
          <h2 class="text-xl font-bold tracking-tight">{{ title }}</h2>
          <button 
            @click="closeDrawer"
            class="p-2 rounded-full hover:bg-slate-100 transition-colors focus:outline-none focus:ring-2 focus:ring-indigo-500"
            data-ce='[{"k":"t-light-class","v":"hover:bg-slate-100"},{"k":"t-dark-class","v":"hover:bg-slate-800"}]'
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>

        <!-- Content Area -->
        <div class="flex-grow p-6 overflow-y-auto">
          <slot></slot>
        </div>
        
        <!-- Footer Area -->
        <div v-if="$slots.footer" class="p-6 border-t"
             data-ce='[{"k":"t-light-class","v":"border-slate-200 bg-slate-50"},{"k":"t-dark-class","v":"border-slate-800 bg-slate-900"}]'
             :class="['border-slate-200 bg-slate-50']"
        >
          <slot name="footer"></slot>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted, watch } from 'vue';
import type { _p_TYP, _pp_TYP } from "../../shared/types";

const props = defineProps<{
    _p: _p_TYP,
    _pp: _pp_TYP,
    isOpen: boolean,
    title?: string
}>();

const emit = defineEmits(['update:isOpen', 'close']);

const closeDrawer = () => {
    emit('update:isOpen', false);
    emit('close');
};

// Prevent background scrolling when drawer is open
watch(() => props.isOpen, (newVal) => {
    if (newVal) {
        document.body.style.overflow = 'hidden';
    } else {
        document.body.style.overflow = '';
    }
});

onUnmounted(() => {
    document.body.style.overflow = '';
});
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.slide-enter-from,
.slide-leave-to {
  transform: translateX(100%);
}
</style>
