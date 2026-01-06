<script setup lang="ts">
// Hero 1: Animated Gradient Wave
// Features a dynamic gradient background with smooth wave animations
// The gradient shifts between colors creating a mesmerizing effect
</script>

<template>
  <section class="relative min-h-screen overflow-hidden bg-gray-900 flex items-center justify-center">
    <!-- Animated gradient background -->
    <div class="absolute inset-0 gradient-wave" />

    <!-- Overlay for better text readability -->
    <div class="absolute inset-0 bg-black/30" />

    <!-- Content -->
    <div class="relative z-10 text-center px-4 max-w-4xl mx-auto">
      <span class="inline-block px-4 py-2 mb-6 text-sm font-medium text-white/90 bg-white/10 backdrop-blur-sm rounded-full border border-white/20">
        Introducing the Future
      </span>

      <h1 class="text-5xl md:text-7xl font-bold text-white mb-6 tracking-tight">
        Build Something
        <span class="block bg-gradient-to-r from-cyan-400 via-purple-500 to-pink-500 bg-clip-text text-transparent">
          Extraordinary
        </span>
      </h1>

      <p class="text-xl md:text-2xl text-white/80 mb-10 max-w-2xl mx-auto leading-relaxed">
        Transform your ideas into reality with cutting-edge tools designed for the modern developer.
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <UButton
          size="xl"
          color="white"
          class="px-8"
        >
          Get Started Free
          <template #trailing>
            <UIcon name="i-lucide-arrow-right" />
          </template>
        </UButton>

        <UButton
          size="xl"
          variant="outline"
          color="white"
          class="px-8"
        >
          <UIcon name="i-lucide-play-circle" class="mr-2" />
          Watch Demo
        </UButton>
      </div>
    </div>

    <!-- Floating particles for depth -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div
        v-for="i in 20"
        :key="i"
        class="particle"
        :style="{
          left: `${Math.random() * 100}%`,
          animationDelay: `${Math.random() * 5}s`,
          animationDuration: `${15 + Math.random() * 10}s`
        }"
      />
    </div>
  </section>
</template>

<style scoped>
/* Animated gradient background using CSS */
.gradient-wave {
  background: linear-gradient(
    -45deg,
    #0f172a,
    #1e1a78,
    #5b21b6,
    #7c3aed,
    #06b6d4,
    #0f172a
  );
  background-size: 400% 400%;
  animation: gradient-shift 15s ease infinite;
}

@keyframes gradient-shift {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Floating particles */
.particle {
  position: absolute;
  width: 4px;
  height: 4px;
  background: white;
  border-radius: 50%;
  opacity: 0.3;
  animation: float-up linear infinite;
}

@keyframes float-up {
  0% {
    transform: translateY(100vh) scale(0);
    opacity: 0;
  }
  10% {
    opacity: 0.3;
  }
  90% {
    opacity: 0.3;
  }
  100% {
    transform: translateY(-10vh) scale(1);
    opacity: 0;
  }
}
</style>
