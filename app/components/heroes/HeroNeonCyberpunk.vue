<script setup lang="ts">
// Hero 10: Neon Cyberpunk Theme
// Bold cyberpunk aesthetic with neon colors, glitch effects, and futuristic vibes
// Features animated scan lines, glowing elements, and high-contrast design
</script>

<template>
  <section class="relative min-h-screen overflow-hidden bg-black">
    <!-- Grid background -->
    <div class="absolute inset-0 grid-bg opacity-30" />

    <!-- Scan lines effect -->
    <div class="absolute inset-0 scan-lines pointer-events-none" />

    <!-- Neon glow spots -->
    <div class="absolute top-0 left-1/4 w-96 h-96 bg-cyan-500/30 rounded-full blur-[150px]" />
    <div class="absolute bottom-0 right-1/4 w-96 h-96 bg-pink-500/30 rounded-full blur-[150px]" />
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-purple-500/20 rounded-full blur-[200px]" />

    <!-- Content -->
    <div class="relative z-10 min-h-screen flex items-center justify-center px-4">
      <div class="max-w-5xl mx-auto text-center">
        <!-- Glitch tag -->
        <div class="mb-8">
          <span class="inline-block px-4 py-2 border border-cyan-500/50 bg-cyan-500/10 text-cyan-400 text-sm font-mono tracking-wider glitch-box">
            [ SYSTEM ONLINE ]
          </span>
        </div>

        <!-- Main heading with glitch effect -->
        <h1 class="text-6xl md:text-8xl lg:text-9xl font-black mb-8 tracking-tighter">
          <span class="block glitch-text" data-text="FUTURE">
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-purple-500 to-pink-500">
              FUTURE
            </span>
          </span>
          <span class="block text-white mt-2 neon-text">
            IS NOW
          </span>
        </h1>

        <!-- Subtitle -->
        <p class="text-xl md:text-2xl text-gray-400 mb-12 max-w-2xl mx-auto font-light tracking-wide">
          Enter the <span class="text-cyan-400">next dimension</span> of digital experience.
          Where reality meets <span class="text-pink-400">imagination</span>.
        </p>

        <!-- CTA buttons -->
        <div class="flex flex-col sm:flex-row gap-6 justify-center mb-16">
          <button class="neon-button cyan group">
            <span class="relative z-10 flex items-center justify-center gap-2">
              <UIcon name="i-lucide-terminal" class="w-5 h-5" />
              INITIALIZE
            </span>
          </button>

          <button class="neon-button pink group">
            <span class="relative z-10 flex items-center justify-center gap-2">
              <UIcon name="i-lucide-scan" class="w-5 h-5" />
              EXPLORE
            </span>
          </button>
        </div>

        <!-- Stats with neon effect -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 max-w-3xl mx-auto">
          <div
            v-for="(stat, index) in [
              { value: '10K+', label: 'Users', color: 'cyan' },
              { value: '99.9%', label: 'Uptime', color: 'pink' },
              { value: '50ms', label: 'Latency', color: 'purple' },
              { value: '24/7', label: 'Support', color: 'yellow' }
            ]"
            :key="index"
            class="stat-card"
          >
            <div
              class="text-3xl md:text-4xl font-black mb-1"
              :class="{
                'text-cyan-400': stat.color === 'cyan',
                'text-pink-400': stat.color === 'pink',
                'text-purple-400': stat.color === 'purple',
                'text-yellow-400': stat.color === 'yellow'
              }"
            >
              {{ stat.value }}
            </div>
            <div class="text-gray-500 text-sm font-mono uppercase tracking-wider">{{ stat.label }}</div>
          </div>
        </div>

        <!-- Bottom decorative element -->
        <div class="mt-20 flex justify-center">
          <div class="flex items-center gap-3 text-gray-600 font-mono text-sm">
            <div class="w-2 h-2 bg-cyan-500 rounded-full animate-pulse" />
            <span>READY FOR CONNECTION</span>
            <div class="w-2 h-2 bg-pink-500 rounded-full animate-pulse" />
          </div>
        </div>
      </div>
    </div>

    <!-- Corner decorations -->
    <div class="absolute top-8 left-8 w-24 h-24 border-l-2 border-t-2 border-cyan-500/50" />
    <div class="absolute top-8 right-8 w-24 h-24 border-r-2 border-t-2 border-pink-500/50" />
    <div class="absolute bottom-8 left-8 w-24 h-24 border-l-2 border-b-2 border-pink-500/50" />
    <div class="absolute bottom-8 right-8 w-24 h-24 border-r-2 border-b-2 border-cyan-500/50" />
  </section>
</template>

<style scoped>
/* Grid background */
.grid-bg {
  background-image:
    linear-gradient(rgba(6, 182, 212, 0.1) 1px, transparent 1px),
    linear-gradient(90deg, rgba(6, 182, 212, 0.1) 1px, transparent 1px);
  background-size: 50px 50px;
}

/* Scan lines */
.scan-lines {
  background: repeating-linear-gradient(
    0deg,
    rgba(0, 0, 0, 0.1) 0px,
    rgba(0, 0, 0, 0.1) 1px,
    transparent 1px,
    transparent 2px
  );
}

/* Glitch text effect */
.glitch-text {
  position: relative;
}

.glitch-text::before,
.glitch-text::after {
  content: attr(data-text);
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: black;
}

.glitch-text::before {
  left: 2px;
  text-shadow: -2px 0 #ff00ff;
  clip-path: inset(20% 0 60% 0);
  animation: glitch-1 2s infinite linear alternate-reverse;
}

.glitch-text::after {
  left: -2px;
  text-shadow: 2px 0 #00ffff;
  clip-path: inset(60% 0 20% 0);
  animation: glitch-2 2s infinite linear alternate-reverse;
}

@keyframes glitch-1 {
  0%, 100% {
    clip-path: inset(20% 0 60% 0);
    transform: translate(0);
  }
  20% {
    clip-path: inset(10% 0 70% 0);
    transform: translate(-2px, 2px);
  }
  40% {
    clip-path: inset(50% 0 30% 0);
    transform: translate(2px, -1px);
  }
  60% {
    clip-path: inset(30% 0 50% 0);
    transform: translate(-1px, 1px);
  }
  80% {
    clip-path: inset(70% 0 10% 0);
    transform: translate(1px, -2px);
  }
}

@keyframes glitch-2 {
  0%, 100% {
    clip-path: inset(60% 0 20% 0);
    transform: translate(0);
  }
  20% {
    clip-path: inset(70% 0 10% 0);
    transform: translate(2px, -2px);
  }
  40% {
    clip-path: inset(30% 0 50% 0);
    transform: translate(-2px, 1px);
  }
  60% {
    clip-path: inset(50% 0 30% 0);
    transform: translate(1px, -1px);
  }
  80% {
    clip-path: inset(10% 0 70% 0);
    transform: translate(-1px, 2px);
  }
}

/* Neon text glow */
.neon-text {
  text-shadow:
    0 0 10px rgba(255, 255, 255, 0.8),
    0 0 20px rgba(255, 255, 255, 0.6),
    0 0 40px rgba(255, 255, 255, 0.4);
}

/* Glitch box */
.glitch-box {
  animation: box-glitch 3s infinite;
}

@keyframes box-glitch {
  0%, 90%, 100% {
    opacity: 1;
    transform: translate(0);
  }
  92% {
    opacity: 0.8;
    transform: translate(-2px, 1px);
  }
  94% {
    opacity: 1;
    transform: translate(2px, -1px);
  }
  96% {
    opacity: 0.9;
    transform: translate(-1px, 2px);
  }
  98% {
    opacity: 1;
    transform: translate(1px, -1px);
  }
}

/* Neon buttons */
.neon-button {
  position: relative;
  padding: 16px 40px;
  font-family: monospace;
  font-weight: bold;
  font-size: 14px;
  letter-spacing: 2px;
  border: 2px solid;
  background: transparent;
  cursor: pointer;
  overflow: hidden;
  transition: all 0.3s ease;
}

.neon-button.cyan {
  color: #06b6d4;
  border-color: #06b6d4;
  box-shadow:
    0 0 10px rgba(6, 182, 212, 0.3),
    inset 0 0 10px rgba(6, 182, 212, 0.1);
}

.neon-button.cyan:hover {
  background: rgba(6, 182, 212, 0.1);
  box-shadow:
    0 0 20px rgba(6, 182, 212, 0.5),
    0 0 40px rgba(6, 182, 212, 0.3),
    inset 0 0 20px rgba(6, 182, 212, 0.2);
}

.neon-button.pink {
  color: #ec4899;
  border-color: #ec4899;
  box-shadow:
    0 0 10px rgba(236, 72, 153, 0.3),
    inset 0 0 10px rgba(236, 72, 153, 0.1);
}

.neon-button.pink:hover {
  background: rgba(236, 72, 153, 0.1);
  box-shadow:
    0 0 20px rgba(236, 72, 153, 0.5),
    0 0 40px rgba(236, 72, 153, 0.3),
    inset 0 0 20px rgba(236, 72, 153, 0.2);
}

/* Stat cards */
.stat-card {
  padding: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
}
</style>
