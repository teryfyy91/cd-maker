<script setup>
import { useCvStore } from '../stores/cvStore'
import { computed } from 'vue'
import { MapPin, Mail, Phone, ExternalLink, Briefcase, Award, BookOpen, Sparkles } from 'lucide-vue-next'

const store = useCvStore()
const cv = computed(() => store.currentCV)
const template = computed(() => store.selectedTemplate)
</script>

<template>
  <div class="w-[210mm] min-h-[297mm] bg-white shadow-2xl transition-all duration-300 cv-document">
    
    <!-- TEMPLATE 1: MOOD BOARD (Creative-1) -->
    <div v-if="template === 'creative-1'" class="p-16 text-slate-800 font-serif animate-in fade-in duration-700">
      <header class="text-center mb-16 border-b-2 border-slate-100 pb-12">
        <h1 class="text-6xl font-black tracking-tighter text-slate-900 mb-6 uppercase">{{ cv.personalInfo.fullName }}</h1>
        <div class="flex justify-center gap-6 text-[10px] font-black uppercase tracking-[0.3em] text-slate-400">
           <span>{{ cv.personalInfo.location }}</span>
           <span>•</span>
           <span>{{ cv.personalInfo.email }}</span>
        </div>
      </header>

      <div class="grid grid-cols-12 gap-12">
        <div class="col-span-8 space-y-12">
           <section>
              <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-indigo-500 mb-6">Vision Statement</h2>
              <p class="text-2xl font-medium leading-relaxed italic text-slate-700 font-serif overflow-hidden">{{ cv.summary }}</p>
           </section>

           <section>
              <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-indigo-500 mb-8 border-b border-indigo-100 pb-2">Professional Experience</h2>
              <div v-for="(exp, idx) in cv.experience" :key="idx" class="mb-10 group">
                 <div class="flex justify-between items-baseline mb-2">
                    <h3 class="text-xl font-bold text-slate-900 group-hover:text-indigo-600 transition-colors">{{ exp.title }}</h3>
                    <span class="text-xs font-black text-slate-300">{{ exp.date }}</span>
                 </div>
                 <p class="text-[10px] font-black uppercase tracking-widest text-slate-400 mb-4">{{ exp.company }}</p>
                 <ul class="space-y-3">
                    <li v-for="(bullet, bIdx) in exp.bullets" :key="bIdx" class="text-sm leading-relaxed text-slate-600 flex gap-3">
                       <span class="text-indigo-300">/</span> {{ bullet }}
                    </li>
                 </ul>
              </div>
           </section>
        </div>

        <div class="col-span-4 space-y-12 bg-slate-50 p-8 rounded-3xl h-fit border border-slate-100">
           <section>
              <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-slate-400 mb-6">Skill Palette</h2>
              <div class="flex flex-wrap gap-2">
                 <span v-for="skill in cv.skills" :key="skill" class="px-3 py-1 bg-white border border-slate-200 text-[10px] font-bold uppercase tracking-wider text-slate-600 rounded-lg">
                    {{ skill }}
                 </span>
              </div>
           </section>

           <section>
              <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-slate-400 mb-6">Education</h2>
              <div v-for="edu in cv.education" :key="edu.school" class="space-y-1">
                 <p class="text-sm font-bold text-slate-800">{{ edu.degree }}</p>
                 <p class="text-xs text-slate-500">{{ edu.school }}</p>
              </div>
           </section>
        </div>
      </div>
    </div>

    <!-- TEMPLATE 2: REBRAND PROPOSAL (Corp-1) -->
    <div v-else-if="template === 'corp-1' || template === 'professional'" class="flex h-full min-h-[297mm] animate-in fade-in duration-700">
      <div class="w-[300px] bg-[#1a1c24] text-white p-10 flex flex-col pt-20">
         <div class="w-16 h-16 bg-indigo-500 rounded-2xl flex items-center justify-center mb-8 shadow-2xl shadow-indigo-500/50">
            <Sparkles class="w-8 h-8 text-white" />
         </div>
         <h1 class="text-3xl font-black tracking-tight leading-none mb-4">{{ cv.personalInfo.fullName.split(' ')[0] }}<br/><span class="text-indigo-400">{{ cv.personalInfo.fullName.split(' ')[1] }}</span></h1>
         
         <div class="mt-auto space-y-6">
            <div class="space-y-4 pt-10 border-t border-white/10">
               <div>
                  <p class="text-[9px] font-black uppercase tracking-[0.3em] text-slate-500 mb-2">Location</p>
                  <p class="text-xs font-bold text-slate-300">{{ cv.personalInfo.location }}</p>
               </div>
               <div>
                  <p class="text-[9px] font-black uppercase tracking-[0.3em] text-slate-500 mb-2">Email</p>
                  <p class="text-xs font-bold text-slate-300 truncate">{{ cv.personalInfo.email }}</p>
               </div>
            </div>
            
            <div class="space-y-3">
               <p class="text-[9px] font-black uppercase tracking-[0.3em] text-slate-500">Inventory</p>
               <div class="flex flex-wrap gap-2">
                  <span v-for="skill in cv.skills" :key="skill" class="px-2.5 py-1 bg-white/5 border border-white/10 text-[9px] font-black uppercase tracking-widest text-indigo-200 rounded-lg">
                     {{ skill }}
                  </span>
               </div>
            </div>
         </div>
      </div>

      <div class="flex-1 p-16 bg-white space-y-16">
         <section>
            <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-slate-300 mb-4">Executive Summary</h2>
            <p class="text-lg font-bold text-slate-800 leading-relaxed font-serif italic">{{ cv.summary }}</p>
         </section>

         <section>
            <h2 class="text-[11px] font-black uppercase tracking-[0.4em] text-slate-300 mb-10">Strategic Experience</h2>
            <div class="space-y-12">
               <div v-for="exp in cv.experience" :key="exp.company" class="relative pl-10 border-l-2 border-slate-100">
                  <div class="absolute -left-[5px] top-1 w-2 h-2 rounded-full bg-indigo-500 ring-4 ring-white"></div>
                  <div class="flex justify-between items-start mb-4">
                     <div>
                        <h3 class="text-xl font-black text-slate-900 tracking-tight">{{ exp.title }}</h3>
                        <p class="text-xs font-bold text-indigo-600 uppercase tracking-widest">{{ exp.company }}</p>
                     </div>
                     <span class="px-3 py-1 bg-slate-50 text-[10px] font-black text-slate-400 rounded-full border border-slate-100">{{ exp.date }}</span>
                  </div>
                  <ul class="space-y-3">
                     <li v-for="bullet in exp.bullets" :key="bullet" class="text-sm text-slate-500 leading-relaxed">{{ bullet }}</li>
                  </ul>
               </div>
            </div>
         </section>
      </div>
    </div>

    <!-- TEMPLATE 3: BRAND GUIDELINES (Min-1) -->
    <div v-else-if="template === 'min-1' || template === 'minimal'" class="p-20 text-slate-900 font-sans animate-in fade-in duration-700 flex flex-col h-full bg-[#f9fafb]">
       <header class="mb-20 grid grid-cols-2 gap-20 items-end">
          <h1 class="text-5xl font-black tracking-tighter uppercase leading-none">{{ cv.personalInfo.fullName }}</h1>
          <div class="text-[10px] font-black uppercase tracking-[0.4em] text-slate-400 space-y-1">
             <p>{{ cv.personalInfo.email }}</p>
             <p>{{ cv.personalInfo.location }}</p>
             <p>{{ cv.personalInfo.linkedin }}</p>
          </div>
       </header>

       <div class="flex-1 space-y-20">
          <section class="grid grid-cols-12 gap-10">
             <div class="col-span-3 text-[10px] font-black uppercase tracking-[0.4em] text-slate-300 mt-1">Profile</div>
             <div class="col-span-9 text-lg font-medium leading-relaxed">{{ cv.summary }}</div>
          </section>

          <section class="grid grid-cols-12 gap-10">
             <div class="col-span-3 text-[10px] font-black uppercase tracking-[0.4em] text-slate-300 mt-1">History</div>
             <div class="col-span-9 space-y-16">
                <div v-for="exp in cv.experience" :key="exp.company">
                   <div class="flex justify-between border-b border-slate-200 pb-4 mb-6">
                      <h3 class="text-xl font-black uppercase tracking-tight">{{ exp.title }}</h3>
                      <span class="text-xs font-black text-slate-400">{{ exp.date }}</span>
                   </div>
                   <p class="text-sm font-bold text-slate-900 mb-6">{{ exp.company }}</p>
                   <ul class="space-y-4">
                      <li v-for="bullet in exp.bullets" :key="bullet" class="text-xs font-medium text-slate-500 leading-relaxed uppercase tracking-widest pl-4 relative">
                         <span class="absolute left-0 top-1.5 w-1.5 h-1.5 bg-slate-200 rounded-full"></span>
                         {{ bullet }}
                      </li>
                   </ul>
                </div>
             </div>
          </section>

          <section class="grid grid-cols-12 gap-10">
             <div class="col-span-3 text-[10px] font-black uppercase tracking-[0.4em] text-slate-300 mt-1">Matrix</div>
             <div class="col-span-9 grid grid-cols-3 gap-6">
                 <div v-for="skill in cv.skills" :key="skill" class="p-4 bg-white border border-slate-100 rounded-2xl">
                    <p class="text-[10px] font-black uppercase tracking-widest text-slate-800">{{ skill }}</p>
                 </div>
             </div>
          </section>
       </div>
    </div>

    <!-- DEFAULT / TECH (Tech-1, Modern-1, Edu-1) -->
    <div v-else class="text-slate-800 font-sans p-16 animate-in fade-in duration-700">
       <div class="bg-indigo-600 p-12 rounded-[2.5rem] text-white mb-16 shadow-2xl shadow-indigo-100">
          <h1 class="text-5xl font-black mb-4">{{ cv.personalInfo.fullName }}</h1>
          <p class="text-indigo-100 max-w-2xl text-lg leading-relaxed">{{ cv.summary }}</p>
       </div>

       <div class="grid grid-cols-10 gap-16">
          <div class="col-span-6 space-y-16">
             <section>
                <div class="flex items-center gap-4 mb-10">
                   <div class="w-10 h-10 bg-indigo-50 rounded-xl flex items-center justify-center text-indigo-600 shadow-sm"><Briefcase class="w-5 h-5" /></div>
                   <h2 class="text-2xl font-black text-slate-900 tracking-tight">Work Experience</h2>
                </div>
                <div class="space-y-12 pl-4 border-l-2 border-indigo-50">
                   <div v-for="exp in cv.experience" :key="exp.company" class="relative">
                      <div class="absolute -left-[27px] top-1.5 w-4 h-4 rounded-full bg-white border-4 border-indigo-500"></div>
                      <h3 class="text-xl font-bold text-slate-900 mb-1">{{ exp.title }}</h3>
                      <p class="text-sm font-semibold text-indigo-600 mb-4">{{ exp.company }} <span class="text-slate-400 ml-2 font-normal">{{ exp.date }}</span></p>
                      <ul class="space-y-2">
                         <li v-for="bullet in exp.bullets" :key="bullet" class="text-sm text-slate-600 leading-relaxed">• {{ bullet }}</li>
                      </ul>
                   </div>
                </div>
             </section>
          </div>

          <div class="col-span-4 space-y-16">
             <section>
                <div class="flex items-center gap-4 mb-10">
                   <div class="w-10 h-10 bg-emerald-50 rounded-xl flex items-center justify-center text-emerald-600 shadow-sm"><Award class="w-5 h-5" /></div>
                   <h2 class="text-2xl font-black text-slate-900 tracking-tight">Expertise</h2>
                </div>
                <div class="flex flex-wrap gap-2">
                   <span v-for="skill in cv.skills" :key="skill" class="px-4 py-2 bg-slate-50 border border-slate-100 text-sm font-bold text-slate-600 rounded-xl">
                      {{ skill }}
                   </span>
                </div>
             </section>
          </div>
       </div>
    </div>

  </div>
</template>

<style scoped>
.cv-document {
  width: 210mm;
  min-height: 297mm;
  box-sizing: border-box;
}
</style>
