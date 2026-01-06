<script setup lang="ts">
// Hero 2: Split Screen Design
// A bold split-screen layout with contrasting colors
// Image on one side, content on the other - great for product showcases
</script>

<template>
  <section class="min-h-screen flex flex-col lg:flex-row">
    <!-- Left side - Content -->
    <div class="flex-1 flex items-center justify-center bg-gray-950 px-6 py-16 lg:py-0">
      <div class="max-w-xl">
        <div class="flex items-center gap-2 mb-6">
          <div class="h-1 w-12 bg-emerald-500 rounded-full" />
          <span class="text-emerald-500 font-semibold text-sm uppercase tracking-wider">
            New Release
          </span>
        </div>

        <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-6 leading-tight">
          Design without
          <span class="text-emerald-400">limits</span>
        </h1>

        <p class="text-lg text-gray-400 mb-8 leading-relaxed">
          Unleash your creativity with tools that adapt to your workflow.
          No constraints, no compromises—just pure creative freedom.
        </p>

        <div class="flex flex-col sm:flex-row gap-4">
          <UButton
            size="xl"
            color="primary"
            class="bg-emerald-500 hover:bg-emerald-600"
          >
            Start Creating
          </UButton>

          <UButton
            size="xl"
            variant="ghost"
            color="white"
          >
            Learn More
            <template #trailing>
              <UIcon name="i-lucide-chevron-right" />
            </template>
          </UButton>
        </div>

        <!-- Stats -->
        <div class="mt-12 pt-8 border-t border-gray-800 grid grid-cols-3 gap-8">
          <div>
            <div class="text-3xl font-bold text-white">50K+</div>
            <div class="text-sm text-gray-500">Active Users</div>
          </div>
          <div>
            <div class="text-3xl font-bold text-white">99.9%</div>
            <div class="text-sm text-gray-500">Uptime</div>
          </div>
          <div>
            <div class="text-3xl font-bold text-white">4.9</div>
            <div class="text-sm text-gray-500">Rating</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Right side - Visual -->
    <div class="flex-1 relative bg-emerald-500 min-h-[50vh] lg:min-h-screen overflow-hidden">
      <!-- Decorative pattern -->
      <div class="absolute inset-0 opacity-20">
        <svg class="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
          <pattern id="grid" width="10" height="10" patternUnits="userSpaceOnUse">
            <circle cx="1" cy="1" r="1" fill="currentColor" />
          </pattern>
          <rect width="100" height="100" fill="url(#grid)" />
        </svg>
      </div>

      <!-- Floating shapes -->
      <div class="absolute inset-0 flex items-center justify-center">
        <div class="relative w-80 h-80">
          <div class="absolute inset-0 bg-white/20 rounded-3xl transform rotate-12 animate-float" />
          <div class="absolute inset-4 bg-white/30 rounded-2xl transform -rotate-6 animate-float-delayed" />
          <div class="absolute inset-8 bg-white rounded-xl shadow-2xl flex items-center justify-center">
            <UIcon name="i-lucide-sparkles" class="w-16 h-16 text-emerald-500" />
          </div>
        </div>
      </div>

      <!-- Corner accent -->
      <div class="absolute -bottom-20 -right-20 w-80 h-80 bg-emerald-600 rounded-full opacity-50" />
    </div>
  </section>
</template>

<style scoped>
@keyframes float {
  0%, 100% {
    transform: translateY(0) rotate(12deg);
  }
  50% {
    transform: translateY(-20px) rotate(12deg);
  }
}

@keyframes float-delayed {
  0%, 100% {
    transform: translateY(0) rotate(-6deg);
  }
  50% {
    transform: translateY(-15px) rotate(-6deg);
  }
}

.animate-float {
  animation: float 6s ease-in-out infinite;
}

.animate-float-delayed {
  animation: float-delayed 6s ease-in-out infinite;
  animation-delay: 0.5s;
}
</style>
