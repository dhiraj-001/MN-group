<template>
  <button 
    @click="handleClick" 
    class="px-6 py-2.5 font-semibold text-sm tracking-wide rounded-full transition-all duration-300 ease-out transform hover:-translate-y-0.5 hover:shadow-lg active:scale-95 flex items-center justify-center gap-2 bg-gradient-to-r from-indigo-500 to-purple-600 text-white shadow-indigo-500/30 hover:shadow-purple-600/40"
    data-ce='[{"k":"t-light-class","v":"bg-gradient-to-r from-indigo-500 to-purple-600 text-white shadow-indigo-500/30 hover:shadow-purple-600/40"},{"k":"t-dark-class","v":"bg-gradient-to-r from-indigo-400 to-purple-500 text-white shadow-indigo-900/50 hover:shadow-purple-500/40"}]'
  >
    {{ buttonText }}
  </button>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import type { _p_TYP, _pp_TYP } from "../../shared/types";

const props = defineProps<{
    _p: _p_TYP,
    _pp: _pp_TYP,
    label?: string
}>();

const emit = defineEmits(['click']);

const buttonText = ref(props.label || 'Click Me');

const handleClick = async () => {
    emit('click');
    
    // Emit an event using the provided system emitter
    if (props._p && props._p.f) {
        await props._p.f.call("msg", {
            type: `button:clicked`,
            _p: props._p,
            _pp: props._pp,
        });
    }
};
</script>

<style scoped>
/* Scoped styles can go here if needed, but Tailwind is preferred */
</style>
