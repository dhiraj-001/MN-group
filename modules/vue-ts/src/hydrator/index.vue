<template>
    <div class="p-8 min-h-screen bg-slate-50 flex justify-center relative" data-ce='[{"k":"t-light-class","v":"bg-slate-50"},{"k":"t-dark-class","v":"bg-slate-900"}]'>
        <div class="max-w-6xl w-full">
            <div class="mb-6 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                <h2 class="text-3xl font-bold text-slate-800 tracking-tight" data-ce='[{"k":"t-light-class","v":"text-slate-800"},{"k":"t-dark-class","v":"text-white"}]'>Featured Products</h2>
                
                <div class="flex flex-col sm:flex-row items-center gap-3 w-full sm:w-auto">
                    <!-- Search Bar -->
                    <SearchBar class="w-full sm:w-64" @search="handleSearch" />

                    <!-- Filter Toggle Button -->
                    <button @click="isFilterDrawerOpen = true" class="w-full sm:w-auto flex justify-center items-center gap-2 px-4 py-2 bg-white border border-slate-200 text-slate-700 font-medium rounded-lg hover:bg-slate-50 hover:text-indigo-600 transition-colors shadow-sm whitespace-nowrap" data-ce='[{"k":"t-light-class","v":"bg-white border-slate-200 text-slate-700 hover:bg-slate-50 hover:text-indigo-600"},{"k":"t-dark-class","v":"bg-slate-800 border-slate-700 text-slate-200 hover:bg-slate-700 hover:text-indigo-400"}]'>
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
                        </svg>
                        Filters
                    </button>
                </div>
            </div>
            
            <!-- Active Filters / Badges Showcase -->
            <div class="flex flex-wrap items-center gap-3 mb-8">
                <span class="text-sm text-slate-500 font-medium" data-ce='[{"k":"t-light-class","v":"text-slate-500"},{"k":"t-dark-class","v":"text-slate-400"}]'>Active Filters:</span>
                <Badge label="Electronics" variant="primary" removable />
                <Badge label="Under $500" variant="warning" removable />
                <Badge label="In Stock" variant="success" removable />
                <button @click="clearAllFilters" class="text-sm text-indigo-600 hover:text-indigo-800 font-medium underline-offset-2 hover:underline transition-colors" data-ce='[{"k":"t-light-class","v":"text-indigo-600 hover:text-indigo-800"},{"k":"t-dark-class","v":"text-indigo-400 hover:text-indigo-300"}]'>Clear all</button>
            </div>
            
            <EmptyState v-if="isEmpty" @action="clearAllFilters" />
            
            <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <Card :_p="_p" :_pp="_pp" @action="openProductDetails" />
                
                <Card 
                    :_p="_p" 
                    :_pp="_pp" 
                    title="Mechanical Keyboard" 
                    description="Premium tactile switches with customizable RGB lighting and an aircraft-grade aluminum frame for ultimate durability."
                    imageUrl="https://images.unsplash.com/photo-1595225476474-87563907a212?q=80&w=800&auto=format&fit=crop"
                    :price="159.00"
                    buttonText="Add to Cart"
                    @action="openProductDetails"
                />
                
                <Card 
                    :_p="_p" 
                    :_pp="_pp" 
                    title="Smart Watch Series 8" 
                    description="Advanced health tracking, Always-On Retina display, and crash detection. Your essential companion for a healthy life."
                    imageUrl="https://images.unsplash.com/photo-1579586337278-3befd40fd17a?q=80&w=800&auto=format&fit=crop"
                    :price="399.00"
                    buttonText="View Details"
                    @action="openProductDetails"
                />
            </div>
        </div>

        <!-- Filter Drawer -->
        <Drawer 
            :_p="_p" 
            :_pp="_pp" 
            v-model:isOpen="isFilterDrawerOpen" 
            title="Filters"
        >
            <FilterPanel />
            
            <template #footer>
                <div class="flex gap-4">
                    <button @click="isFilterDrawerOpen = false" class="flex-1 py-3 px-4 bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold rounded-lg transition-colors" data-ce='[{"k":"t-light-class","v":"bg-slate-200 hover:bg-slate-300 text-slate-800"},{"k":"t-dark-class","v":"bg-slate-800 hover:bg-slate-700 text-slate-200"}]'>
                        Clear All
                    </button>
                    <button @click="isFilterDrawerOpen = false" class="flex-1 py-3 px-4 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-lg shadow-lg shadow-indigo-500/30 transition-colors" data-ce='[{"k":"t-light-class","v":"bg-indigo-600 hover:bg-indigo-700 text-white shadow-indigo-500/30"},{"k":"t-dark-class","v":"bg-indigo-500 hover:bg-indigo-600 text-white shadow-indigo-900/50"}]'>
                        Show Results
                    </button>
                </div>
            </template>
        </Drawer>

        <!-- Product Details Drawer -->
        <Drawer 
            :_p="_p" 
            :_pp="_pp" 
            v-model:isOpen="isDrawerOpen" 
            :title="selectedProduct?.title || 'Product Details'"
        >
            <div v-if="selectedProduct" class="space-y-6">
                <div class="w-full h-64 rounded-xl overflow-hidden shadow-sm">
                    <img :src="selectedProduct.imageUrl" :alt="selectedProduct.title" class="w-full h-full object-cover" />
                </div>
                
                <div>
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-2xl font-bold text-slate-900" data-ce='[{"k":"t-light-class","v":"text-slate-900"},{"k":"t-dark-class","v":"text-white"}]'>
                            ${{ selectedProduct.price }}
                        </h3>
                        <span class="px-3 py-1 bg-green-100 text-green-800 rounded-full text-xs font-semibold uppercase tracking-wider" data-ce='[{"k":"t-light-class","v":"bg-green-100 text-green-800"},{"k":"t-dark-class","v":"bg-green-900/50 text-green-400"}]'>In Stock</span>
                    </div>
                    
                    <h4 class="text-lg font-semibold mb-2 text-slate-800" data-ce='[{"k":"t-light-class","v":"text-slate-800"},{"k":"t-dark-class","v":"text-slate-200"}]'>Description</h4>
                    <p class="text-slate-600 leading-relaxed" data-ce='[{"k":"t-light-class","v":"text-slate-600"},{"k":"t-dark-class","v":"text-slate-400"}]'>
                        {{ selectedProduct.description }}
                    </p>
                </div>
            </div>
            
            <template #footer>
                <div class="flex gap-4">
                    <button @click="isDrawerOpen = false" class="flex-1 py-3 px-4 bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold rounded-lg transition-colors" data-ce='[{"k":"t-light-class","v":"bg-slate-200 hover:bg-slate-300 text-slate-800"},{"k":"t-dark-class","v":"bg-slate-800 hover:bg-slate-700 text-slate-200"}]'>
                        Cancel
                    </button>
                    <button class="flex-1 py-3 px-4 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-lg shadow-lg shadow-indigo-500/30 transition-colors" data-ce='[{"k":"t-light-class","v":"bg-indigo-600 hover:bg-indigo-700 text-white shadow-indigo-500/30"},{"k":"t-dark-class","v":"bg-indigo-500 hover:bg-indigo-600 text-white shadow-indigo-900/50"}]'>
                        Buy Now
                    </button>
                </div>
            </template>
        </Drawer>
    </div>
</template>


<script lang="ts" setup>
import { ref, computed } from 'vue';
import type { _p_TYP, _pp_TYP } from "../shared/types";
import Card from "./src/Card.vue";
import Drawer from "./src/Drawer.vue";
import FilterPanel from "./src/FilterPanel.vue";
import Badge from "./src/Badge.vue";
import SearchBar from "./src/SearchBar.vue";
import EmptyState from "./src/EmptyState.vue";

const {_p,_pp} = defineProps<{
    _p:_p_TYP,
    _pp:_pp_TYP,
}>();

const isDrawerOpen = ref(false);
const isFilterDrawerOpen = ref(false);
const selectedProduct = ref<any>(null);
const searchQuery = ref("");

const isEmpty = computed(() => searchQuery.value.toLowerCase() === 'empty');

const clearAllFilters = () => {
    searchQuery.value = '';
};

const handleSearch = (query: string) => {
    searchQuery.value = query;
    if (_p && _p.f) {
        _p.f.call("msg", {
            type: `search`,
            query: query,
            _p: _p,
            _pp: _pp,
        });
    }
};

const openProductDetails = (product: any) => {
    selectedProduct.value = product;
    isDrawerOpen.value = true;
};

(async () => {
    //==test==//  [START]
    /* await _p.f.wait_until(() => window.location !== null, 50); */

    //1
    _p.my[`emitter`] = _p.f.new_emitter();
    _p.my[`emitter`].on("msg", async (_$:any) => {
        console.log(`_p.my.emitter.on`, _$);
    });
    await _p.my[`emitter`].emit("msg", {
        type: `on:change`,
        _p: _p,
        _pp: _pp,
    });

    
    //2
    _p.f.listen("msg", async (_$) => {
        console.log(`_p.f.listen`, _$);
    });
    setTimeout(async () => {
        await _p.f.call("msg", {
            type: `on:change`,
            _p: _p,
            _pp: _pp,
        });
    }, 500);

    //==test==//  [END]
})();

</script>
