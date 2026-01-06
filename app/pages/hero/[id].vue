<script setup lang="ts">
const route = useRoute()
const heroId = computed(() => route.params.id as string)

const heroComponents: Record<string, Component> = {
  '1-gradient-wave': defineAsyncComponent(() => import('~/components/heroes/HeroGradientWave.vue')),
  '2-split-screen': defineAsyncComponent(() => import('~/components/heroes/HeroSplitScreen.vue')),
  '3-video-background': defineAsyncComponent(() => import('~/components/heroes/HeroVideoBackground.vue')),
  '4-parallax': defineAsyncComponent(() => import('~/components/heroes/HeroParallax.vue')),
  '5-text-reveal': defineAsyncComponent(() => import('~/components/heroes/HeroTextReveal.vue')),
  '6-particles': defineAsyncComponent(() => import('~/components/heroes/HeroParticles.vue')),
  '7-glassmorphism': defineAsyncComponent(() => import('~/components/heroes/HeroGlassmorphism.vue')),
  '8-gradient-mesh': defineAsyncComponent(() => import('~/components/heroes/HeroGradientMesh.vue')),
  '9-floating-cards': defineAsyncComponent(() => import('~/components/heroes/HeroFloatingCards.vue')),
  '10-neon-cyberpunk': defineAsyncComponent(() => import('~/components/heroes/HeroNeonCyberpunk.vue'))
}

const heroNames: Record<string, string> = {
  '1-gradient-wave': 'Gradient Wave',
  '2-split-screen': 'Split Screen',
  '3-video-background': 'Video Background',
  '4-parallax': 'Parallax',
  '5-text-reveal': 'Text Reveal',
  '6-particles': 'Interactive Particles',
  '7-glassmorphism': 'Glassmorphism',
  '8-gradient-mesh': 'Gradient Mesh',
  '9-floating-cards': 'Floating Cards',
  '10-neon-cyberpunk': 'Neon Cyberpunk'
}

const heroIds = Object.keys(heroComponents)
const currentIndex = computed(() => heroIds.indexOf(heroId.value))
const prevHero = computed(() => heroIds[currentIndex.value - 1])
const nextHero = computed(() => heroIds[currentIndex.value + 1])

const currentComponent = computed(() => heroComponents[heroId.value])
const heroName = computed(() => heroNames[heroId.value] || 'Unknown')

// Navigation with keyboard
onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})

const handleKeydown = (e: KeyboardEvent) => {
  if (e.key === 'ArrowRight' && nextHero.value) {
    navigateTo(`/hero/${nextHero.value}`)
  }
  if (e.key === 'ArrowLeft' && prevHero.value) {
    navigateTo(`/hero/${prevHero.value}`)
  }
  if (e.key === 'Escape') {
    navigateTo('/')
  }
}
</script>

<template>
  <div class="relative">
    <!-- Hero Component -->
    <component :is="currentComponent" v-if="currentComponent" />

    <!-- Navigation overlay -->
    <div class="fixed inset-0 z-50 pointer-events-none">
      <!-- Top bar -->
      <div class="absolute top-4 left-1/2 -translate-x-1/2 pointer-events-auto">
        <div class="flex items-center gap-3 px-4 py-2 bg-black/80 backdrop-blur-md rounded-full border border-white/10">
          <NuxtLink
            to="/"
            class="text-white/60 hover:text-white transition"
          >
            <UIcon name="i-lucide-x" class="w-5 h-5" />
          </NuxtLink>
          <span class="text-white/40">|</span>
          <span class="text-white/60 text-sm">
            {{ currentIndex + 1 }} / {{ heroIds.length }}
          </span>
          <span class="text-white/40">•</span>
          <span class="text-white text-sm font-semibold">{{ heroName }}</span>
        </div>
      </div>

      <!-- Prev button -->
      <NuxtLink
        v-if="prevHero"
        :to="`/hero/${prevHero}`"
        class="absolute left-4 top-1/2 -translate-y-1/2 p-3 bg-black/80 backdrop-blur-md rounded-full border border-white/10 text-white hover:bg-black/90 transition pointer-events-auto"
      >
        <UIcon name="i-lucide-chevron-left" class="w-6 h-6" />
      </NuxtLink>

      <!-- Next button -->
      <NuxtLink
        v-if="nextHero"
        :to="`/hero/${nextHero}`"
        class="absolute right-4 top-1/2 -translate-y-1/2 p-3 bg-black/80 backdrop-blur-md rounded-full border border-white/10 text-white hover:bg-black/90 transition pointer-events-auto"
      >
        <UIcon name="i-lucide-chevron-right" class="w-6 h-6" />
      </NuxtLink>

      <!-- Help text -->
      <div class="absolute bottom-4 left-1/2 -translate-x-1/2 text-white/40 text-xs pointer-events-auto">
        ← → to navigate • ESC to go back
      </div>
    </div>
  </div>
</template>
