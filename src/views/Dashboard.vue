<script setup>
import { useRouter } from 'vue-router'
import { Sparkles, FileText, LayoutTemplate, Settings, LogOut, Menu, Zap } from 'lucide-vue-next'
import CVGenerator from '../components/CVGenerator.vue'
import { ref } from 'vue'
import { useAuthStore } from '../stores/authStore'

const router = useRouter()
const authStore = useAuthStore()
const currentTab = ref('cv-builder')

const handleLogout = async () => {
  await authStore.logout()
  router.push('/login')
}

const sidebarItems = [
  { id: 'cv-builder', icon: Zap, label: 'AI Tailor' },
  { id: 'cvs',         icon: FileText, label: 'My CVs' },
  { id: 'templates',  icon: LayoutTemplate, label: 'Templates' },
  { id: 'settings',   icon: Settings, label: 'Settings' },
]
</script>

<template>
  <div class="drawer lg:drawer-open h-screen bg-slate-50 overflow-hidden font-sans">
    <input id="my-drawer-2" type="checkbox" class="drawer-toggle" />
    
    <!-- Page Content -->
    <div class="drawer-content flex flex-col h-full overflow-hidden">
      <!-- Mobile Navbar -->
      <div class="navbar bg-white border-b border-slate-200 lg:hidden shadow-sm flex-none z-30 px-4">
        <div class="flex-none">
          <label for="my-drawer-2" class="btn btn-square btn-ghost drawer-button">
            <Menu class="w-5 h-5" />
          </label>
        </div>
        <div class="flex-1 px-4">
          <span class="font-bold text-lg tracking-tight">AI CV Builder</span>
        </div>
      </div>

      <!-- Main Body -->
      <main class="flex-1 overflow-hidden relative">
        <CVGenerator v-if="currentTab === 'cv-builder'" />
        
        <div v-else class="h-full flex items-center justify-center p-8 bg-slate-50">
          <div class="text-center max-w-sm animate-in fade-in slide-in-from-bottom-4 duration-500">
            <div class="bg-white p-10 rounded-[2.5rem] border border-slate-200 shadow-2xl shadow-slate-200/50">
               <component :is="sidebarItems.find(i => i.id === currentTab)?.icon || FileText" class="w-16 h-16 mx-auto text-primary mb-6 opacity-20" />
               <h2 class="text-2xl font-black mb-3 text-slate-800 uppercase tracking-widest">{{ sidebarItems.find(i => i.id === currentTab)?.label }}</h2>
               <p class="text-slate-500 font-medium leading-relaxed">We're building something special here. This feature will be available in the next update.</p>
               <button @click="currentTab = 'cv-builder'" class="btn btn-primary btn-sm mt-8 rounded-xl px-6">Back to Dashboard</button>
            </div>
          </div>
        </div>
      </main>
    </div>

    <!-- Sidebar -->
    <div class="drawer-side z-50">
      <label for="my-drawer-2" aria-label="close sidebar" class="drawer-overlay"></label>
      <div class="flex flex-col w-[260px] h-full bg-white border-r border-slate-200">
        <!-- Logo -->
        <div class="flex items-center gap-3 p-8 group cursor-pointer" @click="router.push('/')">
          <div class="bg-gradient-to-br from-indigo-600 to-violet-600 p-2.5 rounded-xl text-white shadow-lg shadow-indigo-200 group-hover:scale-110 transition-all duration-300">
            <Sparkles class="w-5 h-5" />
          </div>
          <span class="font-black text-xl tracking-tighter text-slate-900">AI CV Builder</span>
        </div>

        <!-- Navigation -->
        <nav class="flex-1 px-4 py-2 space-y-1">
          <button 
            v-for="item in sidebarItems"
            :key="item.id"
            @click="currentTab = item.id"
            :class="['w-full flex items-center gap-4 px-5 py-3.5 rounded-2xl font-bold transition-all duration-300 group', 
                     currentTab === item.id 
                       ? 'bg-gradient-to-r from-indigo-50 to-white text-indigo-600 shadow-[inset_4px_0_0_0_#4f46e5]' 
                       : 'text-slate-500 hover:bg-slate-50 hover:text-slate-900']"
          >
            <component :is="item.icon" :class="['w-5 h-5 transition-colors', currentTab === item.id ? 'text-indigo-600' : 'text-slate-400 group-hover:text-slate-600']" />
            <span class="text-sm tracking-tight">{{ item.label }}</span>
          </button>
        </nav>

        <!-- Footer section of sidebar -->
        <div class="p-6 space-y-6">
          <!-- Pro Card -->
          <div class="relative group cursor-pointer">
            <div class="absolute -inset-0.5 bg-gradient-to-r from-indigo-600 to-violet-600 rounded-3xl blur opacity-20 group-hover:opacity-40 transition duration-500"></div>
            <div class="relative bg-slate-900 text-white rounded-3xl p-6 overflow-hidden">
              <div class="absolute -top-10 -right-10 w-32 h-32 bg-indigo-500/20 rounded-full blur-3xl"></div>
              <div class="relative z-10">
                <div class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full bg-indigo-500/20 border border-indigo-500/30 mb-4">
                  <div class="w-1.5 h-1.5 rounded-full bg-indigo-400 animate-pulse"></div>
                  <span class="text-[10px] font-black uppercase tracking-widest text-indigo-200">Pro Plan</span>
                </div>
                <p class="text-xs font-medium text-slate-300 mb-5 leading-relaxed">Unlock unlimited AI generation & ATS optimization features.</p>
                <button class="w-full py-2.5 rounded-xl bg-white text-slate-900 text-[11px] font-black uppercase tracking-widest hover:bg-indigo-50 transition-colors">Upgrade Now</button>
              </div>
            </div>
          </div>

          <!-- User Profile -->
          <div class="space-y-4">
            <div class="flex items-center gap-3 p-3 rounded-2xl bg-slate-50 border border-slate-100 group">
              <div class="avatar placeholder shrink-0">
                <div class="bg-indigo-600 text-white rounded-xl w-10 shadow-md">
                  <span class="text-xs font-black">{{ (authStore.user?.email?.[0] ?? 'U').toUpperCase() }}</span>
                </div>
              </div>
              <div class="overflow-hidden">
                <p class="text-xs font-black text-slate-900 truncate tracking-tight uppercase">{{ authStore.user?.email.split('@')[0] }}</p>
                <p class="text-[10px] text-slate-400 font-bold uppercase tracking-widest">Free Account</p>
              </div>
            </div>
            
            <button @click="handleLogout" class="flex items-center gap-3 w-full px-5 py-2 text-slate-400 hover:text-rose-500 transition-colors duration-300 font-bold text-xs uppercase tracking-widest group">
              <LogOut class="w-4 h-4 group-hover:-translate-x-1 transition-transform" />
              Sign Out
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
