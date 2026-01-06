<script setup lang="ts">
const heroes = [
  { id: '1-gradient-wave', name: 'Gradient Wave' },
  { id: '2-split-screen', name: 'Split Screen' },
  { id: '3-video-background', name: 'Video Background' },
  { id: '4-parallax', name: 'Parallax' },
  { id: '5-text-reveal', name: 'Text Reveal' },
  { id: '6-particles', name: 'Interactive Particles' },
  { id: '7-glassmorphism', name: 'Glassmorphism' },
  { id: '8-gradient-mesh', name: 'Gradient Mesh' },
  { id: '9-floating-cards', name: 'Floating Cards' },
  { id: '10-neon-cyberpunk', name: 'Neon Cyberpunk' }
]
</script>

<template>
  <div class="min-h-screen bg-gray-950 py-20">
    <div class="max-w-4xl mx-auto px-4">
      <h1 class="text-4xl md:text-5xl font-bold text-white text-center mb-4">
        10 Vue Powered Heroes
      </h1>
      <p class="text-xl text-gray-400 text-center mb-12">
        Click on any hero to see it in full screen
      </p>

      <div class="grid gap-4">
        <NuxtLink
          v-for="hero in heroes"
          :key="hero.id"
          :to="`/hero/${hero.id}`"
          class="block p-6 bg-gray-900 hover:bg-gray-800 rounded-xl border border-gray-800 hover:border-gray-700 transition group"
        >
          <div class="flex items-center justify-between">
            <div>
              <span class="text-gray-500 text-sm">Hero {{ hero.id.split('-')[0] }}</span>
              <h2 class="text-xl font-semibold text-white">{{ hero.name }}</h2>
            </div>
            <UIcon
              name="i-lucide-arrow-right"
              class="w-6 h-6 text-gray-500 group-hover:text-white group-hover:translate-x-1 transition"
            />
          </div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
