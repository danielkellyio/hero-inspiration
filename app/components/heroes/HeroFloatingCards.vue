<script setup lang="ts">
// Hero 9: Floating Cards Showcase
// 3D floating card layout with hover effects and depth
// Perfect for showcasing products, features, or team members

import { ref, onMounted } from 'vue'

const isLoaded = ref(false)

const cards = [
  {
    icon: 'i-lucide-rocket',
    title: 'Launch Fast',
    description: 'Deploy in minutes with zero configuration',
    color: 'from-blue-500 to-cyan-500'
  },
  {
    icon: 'i-lucide-shield',
    title: 'Secure',
    description: 'Enterprise-grade security built-in',
    color: 'from-purple-500 to-pink-500'
  },
  {
    icon: 'i-lucide-zap',
    title: 'Performant',
    description: 'Optimized for speed at any scale',
    color: 'from-orange-500 to-red-500'
  }
]

onMounted(() => {
  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})
</script>

<template>
  <section class="min-h-screen bg-gradient-to-b from-slate-50 to-white dark:from-slate-950 dark:to-slate-900 py-20 px-4 overflow-hidden">
    <div class="max-w-7xl mx-auto">
      <div class="grid lg:grid-cols-2 gap-16 items-center min-h-[80vh]">
        <!-- Left content -->
        <div
          class="transition-all duration-1000"
          :class="isLoaded ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-12'"
        >
          <div class="inline-flex items-center gap-2 px-4 py-2 mb-6 bg-primary/10 rounded-full">
            <UIcon name="i-lucide-trending-up" class="w-4 h-4 text-primary" />
            <span class="text-sm font-medium text-primary">Growing 200% YoY</span>
          </div>

          <h1 class="text-5xl md:text-6xl lg:text-7xl font-bold text-gray-900 dark:text-white mb-6 leading-tight">
            Build products
            <span class="relative inline-block">
              people
              <svg class="absolute -bottom-2 left-0 w-full h-3 text-primary/30" viewBox="0 0 200 12">
                <path
                  d="M2 8C30 3 60 10 100 6C140 2 170 9 198 5"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="4"
                  stroke-linecap="round"
                />
              </svg>
            </span>
            <span class="text-primary">love</span>
          </h1>

          <p class="text-xl text-gray-600 dark:text-gray-400 mb-8 max-w-lg leading-relaxed">
            Join thousands of teams who ship better products faster with our all-in-one platform.
          </p>

          <div class="flex flex-col sm:flex-row gap-4 mb-12">
            <UButton
              size="xl"
              class="px-8"
            >
              Start Free Trial
              <template #trailing>
                <UIcon name="i-lucide-arrow-right" />
              </template>
            </UButton>

            <UButton
              size="xl"
              variant="soft"
              color="neutral"
              class="px-8"
            >
              <UIcon name="i-lucide-calendar" class="mr-2" />
              Book Demo
            </UButton>
          </div>

          <!-- Trust indicators -->
          <div class="flex items-center gap-6 text-sm text-gray-500 dark:text-gray-400">
            <div class="flex items-center gap-2">
              <UIcon name="i-lucide-check-circle" class="w-5 h-5 text-green-500" />
              <span>Free 14-day trial</span>
            </div>
            <div class="flex items-center gap-2">
              <UIcon name="i-lucide-check-circle" class="w-5 h-5 text-green-500" />
              <span>No credit card</span>
            </div>
          </div>
        </div>

        <!-- Right - Floating cards -->
        <div class="relative h-[500px] lg:h-[600px] perspective-1000">
          <!-- Main feature card -->
          <div
            class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-72 md:w-80 floating-card main-card"
            :class="isLoaded ? 'opacity-100 translate-z-0' : 'opacity-0 translate-z-[-100px]'"
          >
            <div class="bg-white dark:bg-slate-800 rounded-2xl p-8 shadow-2xl border border-gray-100 dark:border-slate-700">
              <div class="w-14 h-14 bg-gradient-to-br from-primary to-primary-600 rounded-xl flex items-center justify-center mb-6">
                <UIcon name="i-lucide-layout-dashboard" class="w-7 h-7 text-white" />
              </div>
              <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">Dashboard</h3>
              <p class="text-gray-600 dark:text-gray-400 mb-6">All your metrics in one place</p>

              <div class="space-y-3">
                <div class="flex items-center justify-between">
                  <span class="text-sm text-gray-500">Revenue</span>
                  <span class="text-sm font-semibold text-green-600">+24%</span>
                </div>
                <div class="h-2 bg-gray-100 dark:bg-slate-700 rounded-full overflow-hidden">
                  <div class="h-full w-3/4 bg-gradient-to-r from-primary to-primary-600 rounded-full" />
                </div>
              </div>
            </div>
          </div>

          <!-- Floating feature cards -->
          <div
            v-for="(card, index) in cards"
            :key="card.title"
            class="absolute floating-card"
            :class="[
              `card-${index + 1}`,
              isLoaded ? 'opacity-100' : 'opacity-0'
            ]"
            :style="{ transitionDelay: `${(index + 1) * 150}ms` }"
          >
            <div class="bg-white dark:bg-slate-800 rounded-xl p-5 shadow-lg border border-gray-100 dark:border-slate-700 w-48">
              <div
                class="w-10 h-10 rounded-lg flex items-center justify-center mb-3 bg-gradient-to-br"
                :class="card.color"
              >
                <UIcon :name="card.icon" class="w-5 h-5 text-white" />
              </div>
              <h4 class="font-semibold text-gray-900 dark:text-white mb-1">{{ card.title }}</h4>
              <p class="text-xs text-gray-500 dark:text-gray-400">{{ card.description }}</p>
            </div>
          </div>

          <!-- Decorative elements -->
          <div class="absolute top-10 right-10 w-20 h-20 bg-primary/10 rounded-full blur-2xl" />
          <div class="absolute bottom-20 left-10 w-32 h-32 bg-purple-500/10 rounded-full blur-3xl" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.perspective-1000 {
  perspective: 1000px;
}

.floating-card {
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.main-card {
  animation: float-main 6s ease-in-out infinite;
  z-index: 10;
}

.card-1 {
  bottom: 5%;
  right: 10%;
  animation: float-1 5s ease-in-out infinite;
}

.card-2 {
  top: 15%;
  right: 5%;
  animation: float-2 7s ease-in-out infinite;
}

.card-3 {
  bottom: 10%;
  left: 5%;
  animation: float-3 6s ease-in-out infinite;
}

@keyframes float-main {
  0%, 100% {
    transform: translate(-50%, -50%) rotateX(5deg) rotateY(-5deg);
  }
  50% {
    transform: translate(-50%, -50%) rotateX(-5deg) rotateY(5deg) translateY(-10px);
  }
}

@keyframes float-1 {
  0%, 100% {
    transform: translateY(0) rotate(-3deg);
  }
  50% {
    transform: translateY(-15px) rotate(3deg);
  }
}

@keyframes float-2 {
  0%, 100% {
    transform: translateY(0) rotate(5deg);
  }
  50% {
    transform: translateY(-20px) rotate(-2deg);
  }
}

@keyframes float-3 {
  0%, 100% {
    transform: translateY(0) rotate(-2deg);
  }
  50% {
    transform: translateY(-12px) rotate(4deg);
  }
}

.floating-card:hover {
  z-index: 20;
  transform: scale(1.05) translateY(-5px) !important;
}
</style>
