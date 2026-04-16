<script setup>
import { useCvStore } from '../stores/cvStore'
import { Sparkles, Check, ChevronRight } from 'lucide-vue-next'

const store = useCvStore()
const emit = defineEmits(['select'])

const templates = [
  { 
    id: 'creative-1', 
    name: 'Mood Board', 
    description: 'Crafting Visual Inspiration', 
    image: 'https://images.unsplash.com/photo-1586717791821-3f44a563cc4c?q=80&w=2070&auto=format&fit=crop', 
    tag: 'Artistic' 
  },
  { 
    id: 'corp-1', 
    name: 'Rebrand Proposal', 
    description: 'Elevating Our Brand', 
    image: 'https://images.unsplash.com/photo-1512486130939-2c4f79935e4f?q=80&w=2070&auto=format&fit=crop', 
    tag: 'Professional' 
  },
  { 
    id: 'min-1', 
    name: 'Brand Guidelines', 
    description: 'Visual Identity System', 
    image: 'https://images.unsplash.com/photo-1434039390530-eb79a46ef42d?q=80&w=2074&auto=format&fit=crop', 
    tag: 'Minimalist' 
  },
  { 
    id: 'tech-1', 
    name: 'Campaign Concept', 
    description: 'Turning Insight into Impact', 
    image: 'https://images.unsplash.com/photo-1616588589676-62b3bd4ff6d2?q=80&w=2072&auto=format&fit=crop', 
    tag: 'Technical' 
  },
  { 
    id: 'edu-1', 
    name: 'Design Sprint Recap', 
    description: 'From Challenge to Solution', 
    image: 'https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?q=80&w=2070&auto=format&fit=crop', 
    tag: 'Academic' 
  },
  { 
    id: 'modern-1', 
    name: 'Professional Portfolio', 
    description: 'Showcasing Your Best Work', 
    image: 'https://images.unsplash.com/photo-1497215121331-739189b537f4?q=80&w=2070&auto=format&fit=crop', 
    tag: 'Trending' 
  }
]

const handleSelect = (templateId) => {
  store.selectedTemplate = templateId
  emit('select')
}
</script>

<template>
  <div class="h-full overflow-y-auto bg-[#daebff] custom-scrollbar pb-32">
    <!-- Immersive Header -->
    <div class="relative pt-24 pb-16 px-12 text-center">
      <div class="max-w-4xl mx-auto space-y-4">
        <h1 class="text-6xl font-black text-[#1a1a1a] tracking-tight leading-[1.05] animate-in fade-in slide-in-from-bottom-4 duration-700">
           Select a template
        </h1>
        <p class="text-[#4a4a4a] text-lg font-medium max-w-xl mx-auto leading-relaxed">
          Start with a professionally designed layout.
        </p>
      </div>
    </div>

    <!-- Gallery Grid -->
    <div class="max-w-[1440px] mx-auto px-12">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
        <div 
          v-for="(tpl, idx) in templates" 
          :key="tpl.id"
          @click="handleSelect(tpl.id)"
          class="group cursor-pointer relative animate-in fade-in slide-in-from-bottom-8 duration-700"
          :style="{ transitionDelay: `${idx * 40}ms` }"
        >
          <div class="space-y-4">
            <div class="relative overflow-hidden rounded-[1.5rem] bg-white shadow-sm transition-all duration-500 group-hover:shadow-2xl group-hover:-translate-y-2">
              
              <!-- Image Area -->
              <div class="aspect-[1.5/1] bg-slate-200 overflow-hidden relative">
                <img 
                  :src="tpl.image" 
                  :alt="tpl.name" 
                  class="w-full h-full object-cover object-center group-hover:scale-110 transition-transform duration-1000"
                />
                
                <!-- Overlay Shadow -->
                <div class="absolute inset-0 bg-gradient-to-t from-black/20 to-transparent group-hover:from-black/40 transition-all duration-500"></div>

                <!-- Gamma Center Hover Button -->
                <div class="absolute inset-0 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-300">
                  <div class="px-6 py-2.5 bg-indigo-600 text-white font-bold rounded-full shadow-2xl flex items-center gap-2 text-sm">
                    View template
                  </div>
                </div>

                <!-- Selection Status -->
                <div v-if="store.selectedTemplate === tpl.id" class="absolute top-4 right-4 w-7 h-7 bg-indigo-600 text-white rounded-full flex items-center justify-center shadow-lg border-2 border-white z-20">
                  <Check class="w-4 h-4 stroke-[3px]" />
                </div>
              </div>
            </div>

            <!-- Card Info -->
            <div class="px-1">
              <h3 class="text-base font-bold text-[#1a1a1a] mb-0.5">{{ tpl.name }}</h3>
              <p class="text-xs text-[#6a6a6a] font-medium">{{ tpl.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.custom-scrollbar::-webkit-scrollbar { width: 6px; }
.custom-scrollbar::-webkit-scrollbar-track { background: transparent; }
.custom-scrollbar::-webkit-scrollbar-thumb { background: rgba(0, 0, 0, 0.05); border-radius: 100px; }
.custom-scrollbar::-webkit-scrollbar-thumb:hover { background: rgba(0, 0, 0, 0.1); }
</style>
