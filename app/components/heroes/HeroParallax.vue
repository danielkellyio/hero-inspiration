<script setup lang="ts">
// Hero 4: Parallax Scrolling Effect
// Multi-layered parallax with depth perception
// Uses scroll-based transforms for a dynamic 3D feel

import { ref, onMounted, onUnmounted } from 'vue'

const scrollY = ref(0)

const handleScroll = () => {
  scrollY.value = window.scrollY
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <section class="relative min-h-[150vh] overflow-hidden bg-slate-950">
    <!-- Background layer - slowest -->
    <div
      class="absolute inset-0 bg-gradient-to-b from-indigo-950 to-slate-950"
      :style="{ transform: `translateY(${scrollY * 0.1}px)` }"
    />

    <!-- Stars layer -->
    <div
      class="absolute inset-0"
      :style="{ transform: `translateY(${scrollY * 0.2}px)` }"
    >
      <div
        v-for="i in 50"
        :key="`star-${i}`"
        class="absolute w-1 h-1 bg-white rounded-full opacity-60"
        :style="{
          left: `${Math.random() * 100}%`,
          top: `${Math.random() * 100}%`,
          animationDelay: `${Math.random() * 3}s`
        }"
      />
    </div>

    <!-- Mountain silhouette - back -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.3}px)` }"
    >
      <svg class="w-full" viewBox="0 0 1440 400" fill="none" preserveAspectRatio="none">
        <path
          d="M0 400L0 300L200 200L400 280L600 150L800 250L1000 100L1200 220L1440 180L1440 400Z"
          fill="#1e1b4b"
        />
      </svg>
    </div>

    <!-- Mountain silhouette - front -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.5}px)` }"
    >
      <svg class="w-full" viewBox="0 0 1440 320" fill="none" preserveAspectRatio="none">
        <path
          d="M0 320L0 250L150 180L350 240L500 120L700 200L900 80L1100 180L1300 140L1440 200L1440 320Z"
          fill="#0f172a"
        />
      </svg>
    </div>

    <!-- Content - fastest (fixed feeling) -->
    <div class="sticky top-0 min-h-screen flex items-center justify-center px-4">
      <div class="text-center max-w-4xl">
        <!-- Planet/Moon accent -->
        <div
          class="absolute top-20 right-10 md:right-1/4 w-24 h-24 md:w-32 md:h-32 rounded-full bg-gradient-to-br from-orange-300 to-orange-500 opacity-80 blur-sm"
          :style="{ transform: `translateY(${scrollY * 0.4}px)` }"
        />

        <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold text-white mb-6 relative z-10">
          <span class="block">Explore</span>
          <span class="block bg-gradient-to-r from-purple-400 to-pink-400 bg-clip-text text-transparent">
            New Heights
          </span>
        </h1>

        <p class="text-xl md:text-2xl text-slate-300 mb-10 max-w-2xl mx-auto relative z-10">
          Journey through landscapes of innovation. Every scroll reveals new possibilities.
        </p>

        <div class="flex flex-col sm:flex-row gap-4 justify-center relative z-10">
          <UButton
            size="xl"
            class="bg-gradient-to-r from-purple-500 to-pink-500 hover:from-purple-600 hover:to-pink-600 border-0 px-8"
          >
            Begin Journey
            <template #trailing>
              <UIcon name="i-lucide-rocket" />
            </template>
          </UButton>

          <UButton
            size="xl"
            variant="outline"
            color="white"
            class="border-white/30 hover:bg-white/10 px-8"
          >
            View Map
          </UButton>
        </div>

        <!-- Scroll hint -->
        <div class="mt-20 text-slate-500 text-sm">
          <UIcon name="i-lucide-mouse" class="w-5 h-5 mb-2 mx-auto animate-bounce" />
          <p>Scroll to explore the parallax effect</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.star {
  animation: twinkle 3s ease-in-out infinite;
}

@keyframes twinkle {
  0%, 100% {
    opacity: 0.3;
  }
  50% {
    opacity: 1;
  }
}
</style>
