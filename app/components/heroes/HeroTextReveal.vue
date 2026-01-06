<script setup lang="ts">
// Hero 5: Animated Text Reveal
// Sophisticated text animations with staggered reveals
// Uses CSS animations and Vue transitions for smooth effects

import { ref, onMounted } from 'vue'

const isLoaded = ref(false)
const words = ['Innovate', 'Create', 'Transform']
const currentWordIndex = ref(0)

onMounted(() => {
  isLoaded.value = true

  // Cycle through words
  setInterval(() => {
    currentWordIndex.value = (currentWordIndex.value + 1) % words.length
  }, 3000)
})
</script>

<template>
  <section class="min-h-screen bg-white dark:bg-gray-950 flex items-center justify-center px-4 overflow-hidden">
    <div class="max-w-6xl mx-auto text-center">
      <!-- Decorative elements -->
      <div class="absolute top-20 left-10 w-64 h-64 bg-purple-200 dark:bg-purple-900/30 rounded-full blur-3xl opacity-50" />
      <div class="absolute bottom-20 right-10 w-96 h-96 bg-blue-200 dark:bg-blue-900/30 rounded-full blur-3xl opacity-50" />

      <!-- Tag line with reveal -->
      <div
        class="overflow-hidden mb-6"
        :class="isLoaded ? 'opacity-100' : 'opacity-0'"
      >
        <span
          class="inline-block text-sm font-semibold tracking-widest uppercase text-purple-600 dark:text-purple-400 transition-transform duration-700"
          :class="isLoaded ? 'translate-y-0' : 'translate-y-full'"
        >
          Welcome to the future
        </span>
      </div>

      <!-- Main heading with word animation -->
      <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold mb-8 relative">
        <span
          class="block text-gray-900 dark:text-white transition-all duration-700 delay-100"
          :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
        >
          We help you
        </span>

        <!-- Animated word cycler -->
        <span class="relative inline-block h-[1.2em] overflow-hidden">
          <TransitionGroup
            tag="span"
            enter-active-class="transition-all duration-500"
            enter-from-class="opacity-0 translate-y-full"
            enter-to-class="opacity-100 translate-y-0"
            leave-active-class="transition-all duration-500 absolute inset-0"
            leave-from-class="opacity-100 translate-y-0"
            leave-to-class="opacity-0 -translate-y-full"
          >
            <span
              v-for="(word, index) in words"
              v-show="currentWordIndex === index"
              :key="word"
              class="bg-gradient-to-r from-purple-600 via-pink-600 to-blue-600 bg-clip-text text-transparent"
            >
              {{ word }}
            </span>
          </TransitionGroup>
        </span>
      </h1>

      <!-- Description with staggered reveal -->
      <p
        class="text-xl md:text-2xl text-gray-600 dark:text-gray-400 max-w-3xl mx-auto mb-12 transition-all duration-700 delay-300"
        :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
      >
        Empowering businesses with cutting-edge solutions that drive growth,
        efficiency, and lasting impact in the digital age.
      </p>

      <!-- CTA with reveal -->
      <div
        class="flex flex-col sm:flex-row gap-4 justify-center transition-all duration-700 delay-500"
        :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
      >
        <UButton
          size="xl"
          class="bg-gray-900 dark:bg-white text-white dark:text-gray-900 hover:bg-gray-800 dark:hover:bg-gray-100 px-10"
        >
          Get Started
          <template #trailing>
            <UIcon name="i-lucide-arrow-right" />
          </template>
        </UButton>

        <UButton
          size="xl"
          variant="outline"
          color="neutral"
          class="px-10"
        >
          Book a Demo
        </UButton>
      </div>

      <!-- Floating badges with animations -->
      <div
        class="mt-20 flex flex-wrap justify-center gap-4 transition-all duration-700 delay-700"
        :class="isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
      >
        <span
          v-for="(badge, i) in ['Trusted by 500+ companies', '99.9% uptime', '24/7 support', 'SOC 2 compliant']"
          :key="badge"
          class="inline-flex items-center gap-2 px-4 py-2 bg-gray-100 dark:bg-gray-800 rounded-full text-sm text-gray-700 dark:text-gray-300"
          :style="{ transitionDelay: `${700 + i * 100}ms` }"
        >
          <UIcon name="i-lucide-check-circle" class="w-4 h-4 text-green-500" />
          {{ badge }}
        </span>
      </div>
    </div>
  </section>
</template>
