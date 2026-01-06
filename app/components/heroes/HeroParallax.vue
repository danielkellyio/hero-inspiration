<script setup lang="ts">
// Hero 4: Layered Paper-Cut Parallax
// A warm, artistic parallax effect with silhouetted layers
// Creates depth through overlapping organic shapes at different scroll speeds

import { ref, onMounted, onUnmounted } from 'vue'

const scrollY = ref(0)
const containerRef = ref<HTMLElement | null>(null)

const handleScroll = () => {
  scrollY.value = window.scrollY
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <section ref="containerRef" class="relative min-h-[200vh] overflow-hidden">
    <!-- Sky gradient - slowest layer -->
    <div
      class="absolute inset-0 sky-gradient"
      :style="{ transform: `translateY(${scrollY * 0.05}px)` }"
    />

    <!-- Sun/moon orb -->
    <div
      class="absolute left-1/2 -translate-x-1/2 top-[15%] w-32 h-32 md:w-48 md:h-48"
      :style="{ transform: `translateX(-50%) translateY(${scrollY * 0.15}px)` }"
    >
      <div class="w-full h-full rounded-full bg-gradient-to-b from-amber-200 to-orange-300 blur-sm" />
      <div class="absolute inset-2 rounded-full bg-gradient-to-b from-amber-100 to-amber-200" />
    </div>

    <!-- Distant clouds layer -->
    <div
      class="absolute inset-0"
      :style="{ transform: `translateY(${scrollY * 0.1}px)` }"
    >
      <svg class="absolute top-[20%] left-[10%] w-48 h-16 opacity-40" viewBox="0 0 200 60">
        <ellipse cx="50" cy="40" rx="40" ry="20" fill="#fef3c7" />
        <ellipse cx="90" cy="35" rx="50" ry="25" fill="#fef3c7" />
        <ellipse cx="140" cy="40" rx="35" ry="18" fill="#fef3c7" />
      </svg>
      <svg class="absolute top-[25%] right-[15%] w-36 h-12 opacity-30" viewBox="0 0 150 50">
        <ellipse cx="40" cy="30" rx="35" ry="18" fill="#fef3c7" />
        <ellipse cx="85" cy="28" rx="40" ry="20" fill="#fef3c7" />
      </svg>
    </div>

    <!-- Distant hills - Layer 1 -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.2}px)` }"
    >
      <svg class="w-full h-auto" viewBox="0 0 1440 400" preserveAspectRatio="none" fill="none">
        <path
          d="M0 400V280C120 250 240 300 400 260C560 220 680 280 840 240C1000 200 1160 260 1280 230C1360 210 1400 240 1440 220V400H0Z"
          class="fill-rose-300/60"
        />
      </svg>
    </div>

    <!-- Mid hills - Layer 2 -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.35}px)` }"
    >
      <svg class="w-full h-auto" viewBox="0 0 1440 350" preserveAspectRatio="none" fill="none">
        <path
          d="M0 350V200C100 240 200 180 350 210C500 240 600 160 750 200C900 240 1050 170 1200 210C1300 235 1380 200 1440 220V350H0Z"
          class="fill-rose-400/70"
        />
      </svg>
    </div>

    <!-- Trees layer - Layer 3 -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.5}px)` }"
    >
      <svg class="w-full h-auto" viewBox="0 0 1440 300" preserveAspectRatio="none" fill="none">
        <!-- Base hill -->
        <path
          d="M0 300V180C150 200 300 150 450 170C600 190 750 140 900 165C1050 190 1200 145 1350 170C1400 178 1420 175 1440 180V300H0Z"
          class="fill-rose-700/80"
        />
        <!-- Tree silhouettes -->
        <path d="M80 180L100 120L120 180Z" class="fill-rose-800" />
        <path d="M90 180L100 140L110 180Z" class="fill-rose-900" />
        <path d="M200 170L230 90L260 170Z" class="fill-rose-800" />
        <path d="M215 170L230 110L245 170Z" class="fill-rose-900" />
        <path d="M350 165L370 100L390 165Z" class="fill-rose-800" />
        <path d="M500 175L525 95L550 175Z" class="fill-rose-800" />
        <path d="M510 175L525 120L540 175Z" class="fill-rose-900" />
        <path d="M700 160L730 70L760 160Z" class="fill-rose-800" />
        <path d="M715 160L730 100L745 160Z" class="fill-rose-900" />
        <path d="M900 170L920 110L940 170Z" class="fill-rose-800" />
        <path d="M1050 165L1080 80L1110 165Z" class="fill-rose-800" />
        <path d="M1065 165L1080 105L1095 165Z" class="fill-rose-900" />
        <path d="M1250 175L1270 115L1290 175Z" class="fill-rose-800" />
        <path d="M1380 180L1400 130L1420 180Z" class="fill-rose-800" />
      </svg>
    </div>

    <!-- Foreground layer - closest, fastest -->
    <div
      class="absolute bottom-0 left-0 right-0"
      :style="{ transform: `translateY(${scrollY * 0.7}px)` }"
    >
      <svg class="w-full h-auto" viewBox="0 0 1440 200" preserveAspectRatio="none" fill="none">
        <path
          d="M0 200V120C80 100 160 130 280 110C400 90 520 120 640 100C760 80 880 115 1000 95C1120 75 1240 110 1360 90C1400 85 1420 95 1440 90V200H0Z"
          class="fill-rose-950"
        />
        <!-- Grass/plant silhouettes -->
        <g class="fill-rose-950">
          <path d="M30 120C30 120 35 100 40 120C40 120 45 95 50 120" />
          <path d="M150 110C150 110 158 85 165 110" />
          <path d="M300 105C300 105 310 75 320 105C320 105 330 80 340 105" />
          <path d="M500 100C500 100 510 70 520 100" />
          <path d="M700 95C700 95 715 60 730 95C730 95 745 65 760 95" />
          <path d="M950 100C950 100 960 75 970 100" />
          <path d="M1150 95C1150 95 1165 60 1180 95" />
          <path d="M1350 100C1350 100 1365 70 1380 100C1380 100 1395 75 1410 100" />
        </g>
      </svg>
    </div>

    <!-- Flying birds at different speeds -->
    <div
      v-for="i in 5"
      :key="`bird-${i}`"
      class="absolute bird"
      :style="{
        left: `${10 + i * 18}%`,
        top: `${15 + (i % 3) * 8}%`,
        transform: `translateY(${scrollY * (0.1 + i * 0.05)}px) translateX(${scrollY * 0.1}px)`,
        opacity: 0.6 - i * 0.08
      }"
    >
      <svg :width="20 + i * 4" :height="12 + i * 2" viewBox="0 0 24 12" fill="none">
        <path d="M0 6C4 2 8 4 12 6C16 4 20 2 24 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" class="text-rose-800" />
      </svg>
    </div>

    <!-- Content - sticky -->
    <div class="sticky top-0 min-h-screen flex items-center justify-center px-4 pt-16">
      <div class="text-center max-w-3xl relative z-10">
        <div class="mb-6">
          <span class="inline-flex items-center gap-2 px-4 py-2 bg-white/20 backdrop-blur-sm rounded-full text-rose-900 text-sm font-medium border border-rose-200/30">
            <span class="w-2 h-2 bg-amber-500 rounded-full animate-pulse" />
            Scroll to explore
          </span>
        </div>

        <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold mb-6 tracking-tight">
          <span class="block text-rose-950 drop-shadow-sm">Chase the</span>
          <span class="block text-transparent bg-clip-text bg-gradient-to-r from-amber-500 via-orange-500 to-rose-500">
            Horizon
          </span>
        </h1>

        <p class="text-lg md:text-xl text-rose-900/80 mb-10 max-w-xl mx-auto leading-relaxed font-light">
          Layers of depth reveal themselves as you journey forward. Each scroll brings new perspectives.
        </p>

        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton
            size="xl"
            class="bg-gradient-to-r from-rose-600 to-orange-500 hover:from-rose-700 hover:to-orange-600 text-white border-0 shadow-lg shadow-rose-500/25 px-8"
          >
            Start Journey
            <template #trailing>
              <UIcon name="i-lucide-compass" />
            </template>
          </UButton>

          <UButton
            size="xl"
            variant="outline"
            class="border-rose-400/50 text-rose-800 hover:bg-rose-100/50 backdrop-blur-sm px-8"
          >
            <UIcon name="i-lucide-map" class="mr-2" />
            View Path
          </UButton>
        </div>

        <!-- Scroll indicator -->
        <div class="mt-16 flex flex-col items-center gap-2 text-rose-600/60">
          <div class="w-6 h-10 border-2 border-rose-400/40 rounded-full flex justify-center pt-2">
            <div class="w-1.5 h-3 bg-rose-500/60 rounded-full animate-bounce" />
          </div>
          <span class="text-xs uppercase tracking-widest font-medium">Scroll Down</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.sky-gradient {
  background: linear-gradient(
    180deg,
    #fef3c7 0%,
    #fde68a 15%,
    #fdba74 35%,
    #fb923c 50%,
    #f97316 65%,
    #ea580c 80%,
    #c2410c 100%
  );
}

.bird {
  animation: bird-float 4s ease-in-out infinite;
}

.bird:nth-child(2) { animation-delay: 0.5s; }
.bird:nth-child(3) { animation-delay: 1s; }
.bird:nth-child(4) { animation-delay: 1.5s; }
.bird:nth-child(5) { animation-delay: 2s; }

@keyframes bird-float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}
</style>
