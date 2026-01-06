<script setup lang="ts">
// Hero 8: Animated Gradient Mesh
// Complex gradient mesh background with organic shapes
// Creates a fluid, dynamic visual effect with smooth color transitions
</script>

<template>
  <section class="relative min-h-screen overflow-hidden bg-black">
    <!-- Animated mesh gradient background -->
    <div class="absolute inset-0">
      <!-- Base gradient -->
      <div class="absolute inset-0 bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900" />

      <!-- Mesh blobs -->
      <div class="mesh-container">
        <div class="mesh-blob mesh-1" />
        <div class="mesh-blob mesh-2" />
        <div class="mesh-blob mesh-3" />
        <div class="mesh-blob mesh-4" />
        <div class="mesh-blob mesh-5" />
      </div>

      <!-- Noise overlay for texture -->
      <div class="absolute inset-0 opacity-20 mix-blend-overlay noise-bg" />
    </div>

    <!-- Content -->
    <div class="relative z-10 min-h-screen flex flex-col items-center justify-center px-4">
      <div class="text-center max-w-5xl">
        <!-- Eyebrow -->
        <div class="mb-8">
          <span class="inline-flex items-center gap-3 px-5 py-2.5 bg-white/5 backdrop-blur-sm border border-white/10 rounded-full">
            <span class="flex items-center gap-1.5">
              <span class="w-1.5 h-1.5 bg-emerald-400 rounded-full animate-pulse" />
              <span class="text-emerald-400 text-sm font-medium">New</span>
            </span>
            <span class="text-white/60 text-sm">Version 2.0 is here</span>
            <UIcon name="i-lucide-arrow-right" class="w-4 h-4 text-white/40" />
          </span>
        </div>

        <!-- Main heading -->
        <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold mb-8 leading-none tracking-tight">
          <span class="block text-white">Design that</span>
          <span class="block text-transparent bg-clip-text mesh-text-gradient">
            moves you
          </span>
        </h1>

        <!-- Description -->
        <p class="text-xl md:text-2xl text-white/60 mb-12 max-w-2xl mx-auto leading-relaxed">
          Create immersive experiences with fluid, organic gradients that bring your vision to life.
        </p>

        <!-- CTAs -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center mb-16">
          <UButton
            size="xl"
            class="mesh-button px-10 py-4"
          >
            Start Creating
            <template #trailing>
              <UIcon name="i-lucide-arrow-right" />
            </template>
          </UButton>

          <UButton
            size="xl"
            variant="ghost"
            class="text-white/80 hover:text-white hover:bg-white/5 px-10"
          >
            <UIcon name="i-lucide-play-circle" class="mr-2" />
            Watch Video
          </UButton>
        </div>

        <!-- Logos/Social proof -->
        <div class="pt-8 border-t border-white/10">
          <p class="text-white/40 text-sm mb-6">Trusted by innovative teams worldwide</p>
          <div class="flex flex-wrap justify-center items-center gap-8 opacity-50">
            <div
              v-for="i in 5"
              :key="i"
              class="flex items-center gap-2 text-white/60"
            >
              <UIcon name="i-lucide-hexagon" class="w-6 h-6" />
              <span class="font-semibold">Company {{ i }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom wave decoration -->
    <div class="absolute bottom-0 left-0 right-0">
      <svg class="w-full h-24 fill-white/5" viewBox="0 0 1440 100" preserveAspectRatio="none">
        <path d="M0,50 C360,100 720,0 1080,50 C1260,75 1380,75 1440,50 L1440,100 L0,100 Z" />
      </svg>
    </div>
  </section>
</template>

<style scoped>
.mesh-container {
  position: absolute;
  inset: 0;
  filter: blur(80px);
  opacity: 0.8;
}

.mesh-blob {
  position: absolute;
  border-radius: 50%;
}

.mesh-1 {
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, #7c3aed 0%, transparent 70%);
  top: -10%;
  left: 10%;
  animation: mesh-float-1 20s ease-in-out infinite;
}

.mesh-2 {
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, #ec4899 0%, transparent 70%);
  top: 20%;
  right: 5%;
  animation: mesh-float-2 18s ease-in-out infinite;
}

.mesh-3 {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, #06b6d4 0%, transparent 70%);
  bottom: 10%;
  left: 20%;
  animation: mesh-float-3 22s ease-in-out infinite;
}

.mesh-4 {
  width: 350px;
  height: 350px;
  background: radial-gradient(circle, #f97316 0%, transparent 70%);
  bottom: 30%;
  right: 25%;
  animation: mesh-float-4 16s ease-in-out infinite;
}

.mesh-5 {
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, #22c55e 0%, transparent 70%);
  top: 40%;
  left: 40%;
  animation: mesh-float-5 24s ease-in-out infinite;
}

@keyframes mesh-float-1 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(50px, 30px) scale(1.1); }
  66% { transform: translate(-30px, 50px) scale(0.95); }
}

@keyframes mesh-float-2 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(-40px, 40px) scale(0.9); }
  66% { transform: translate(30px, -30px) scale(1.05); }
}

@keyframes mesh-float-3 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(60px, -40px) scale(1.15); }
  66% { transform: translate(-50px, 30px) scale(0.9); }
}

@keyframes mesh-float-4 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(-30px, -50px) scale(1.1); }
  66% { transform: translate(40px, 20px) scale(0.95); }
}

@keyframes mesh-float-5 {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(30px, 60px) scale(0.85); }
  66% { transform: translate(-60px, -20px) scale(1.1); }
}

.mesh-text-gradient {
  background: linear-gradient(135deg, #7c3aed, #ec4899, #06b6d4, #7c3aed);
  background-size: 300% 300%;
  animation: text-gradient 8s ease infinite;
}

@keyframes text-gradient {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.mesh-button {
  background: linear-gradient(135deg, #7c3aed, #ec4899);
  border: none;
  position: relative;
  overflow: hidden;
}

.mesh-button::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, #ec4899, #7c3aed);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.mesh-button:hover::before {
  opacity: 1;
}

.noise-bg {
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}
</style>
