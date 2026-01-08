<script setup lang="ts">
// Hero 1: Animated Gradient Wave
// Features a dynamic gradient background with smooth wave animations
// Cool ocean blues with warm amber/orange accents for striking contrast
</script>

<template>
  <section class="relative min-h-screen overflow-hidden bg-slate-950 flex items-center justify-center">
    <!-- Animated gradient background -->
    <div class="absolute inset-0 gradient-wave" />

    <!-- Overlay for better text readability -->
    <div class="absolute inset-0 bg-black/25" />

    <!-- Content -->
    <div class="relative z-10 text-center px-4 max-w-4xl mx-auto">
      <h1 class="text-5xl md:text-7xl font-bold text-white mb-6 tracking-tight">
        Build Something
        <span class="block bg-gradient-to-r from-amber-400 via-orange-500 to-rose-500 bg-clip-text text-transparent">
          Extraordinary
        </span>
      </h1>

      <p class="text-xl md:text-2xl text-white/80 mb-10 max-w-2xl mx-auto leading-relaxed">
        Transform your ideas into reality with cutting-edge tools designed for the modern developer.
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <button class="primary-btn group">
          <span class="relative z-10 flex items-center gap-2">
            Get Started Free
            <UIcon name="i-lucide-arrow-right" class="w-5 h-5 transition-transform group-hover:translate-x-1" />
          </span>
        </button>

        <button class="secondary-btn group">
          <UIcon name="i-lucide-play-circle" class="w-5 h-5 mr-2" />
          Watch Demo
        </button>
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
/* Animated gradient background using CSS - deep ocean palette with more contrast */
.gradient-wave {
  background: linear-gradient(
    -45deg,
    #0f172a,
    #1e3a8a,
    #1d4ed8,
    #0e7490,
    #134e4a,
    #0f172a
  );
  background-size: 400% 400%;
  animation: gradient-shift 18s ease infinite;
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

/* Primary button with warm gradient background */
.primary-btn {
  display: inline-flex;
  align-items: center;
  padding: 16px 32px;
  font-size: 16px;
  font-weight: 600;
  color: white;
  background: linear-gradient(135deg, #f59e0b, #ea580c, #dc2626);
  border: none;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 0 4px 20px rgba(234, 88, 12, 0.4);
  transition: all 0.3s ease;
}

.primary-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(234, 88, 12, 0.5), 0 0 0 4px rgba(234, 88, 12, 0.15);
}

/* Secondary button with glass effect */
.secondary-btn {
  display: inline-flex;
  align-items: center;
  padding: 16px 32px;
  font-size: 16px;
  font-weight: 600;
  color: white;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.secondary-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.4);
  transform: translateY(-2px);
}

/* Floating particles with warm glow */
.particle {
  position: absolute;
  width: 4px;
  height: 4px;
  background: linear-gradient(135deg, #fbbf24, #f97316);
  border-radius: 50%;
  opacity: 0.5;
  box-shadow: 0 0 8px rgba(251, 191, 36, 0.5);
  animation: float-up linear infinite;
}

@keyframes float-up {
  0% {
    transform: translateY(100vh) scale(0);
    opacity: 0;
  }
  10% {
    opacity: 0.5;
  }
  90% {
    opacity: 0.5;
  }
  100% {
    transform: translateY(-10vh) scale(1);
    opacity: 0;
  }
}
</style>
