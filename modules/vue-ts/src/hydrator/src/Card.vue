<template>
  <div 
    class="w-full max-w-sm rounded-2xl overflow-hidden shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl bg-white border border-gray-100 flex flex-col"
    data-ce='[{"k":"t-light-class","v":"bg-white border-gray-100 shadow-lg"},{"k":"t-dark-class","v":"bg-slate-800 border-slate-700 shadow-slate-900/50"}]'
  >
    <!-- Image Header -->
    <div class="relative h-56 overflow-hidden bg-gray-100 group">
      <img :src="imageUrl" :alt="title" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110" />
      
      <!-- Price Badge -->
      <div class="absolute top-4 right-4 bg-white/90 backdrop-blur-md px-3 py-1 rounded-full text-sm font-bold text-gray-900 shadow-sm z-10">
        ${{ price }}
      </div>
    </div>
    
    <!-- Content Body -->
    <div class="p-6 flex flex-col flex-grow">
      <h3 
        class="text-xl font-bold mb-2 text-gray-900 tracking-tight"
        data-ce='[{"k":"t-light-class","v":"text-gray-900"},{"k":"t-dark-class","v":"text-white"}]'
      >
        {{ title }}
      </h3>
      
      <p 
        class="text-gray-600 text-sm mb-6 flex-grow line-clamp-3 leading-relaxed"
        data-ce='[{"k":"t-light-class","v":"text-gray-600"},{"k":"t-dark-class","v":"text-slate-300"}]'
      >
        {{ description }}
      </p>
      
      <!-- Action Footer -->
      <div class="mt-auto pt-2 flex w-full">
         <Button @click="$emit('action', {title, description, price, imageUrl})" :_p="_p" :_pp="_pp" :label="buttonText" class="w-full" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { _p_TYP, _pp_TYP } from "../../shared/types";
import Button from "./Button.vue";

const props = defineProps<{
    _p: _p_TYP,
    _pp: _pp_TYP,
    title?: string,
    description?: string,
    imageUrl?: string,
    price?: number,
    buttonText?: string
}>();

const emit = defineEmits(['action']);

const title = props.title || "Premium Wireless Headphones";
const description = props.description || "Experience crystal-clear audio with our industry-leading noise cancellation. Features 30-hour battery life and supreme comfort.";
const imageUrl = props.imageUrl || "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?q=80&w=800&auto=format&fit=crop";
const price = props.price || 299.99;
const buttonText = props.buttonText || "View Details";
</script>
