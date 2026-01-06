<script setup lang="ts">
// Hero 3: Video Background
// Full-screen video background with overlay and centered content
// Uses a placeholder video - replace with actual video in production

const videoUrl = 'https://videos.pexels.com/video-files/3129671/3129671-uhd_2560_1440_30fps.mp4'
</script>

<template>
  <section class="relative min-h-screen overflow-hidden flex items-center justify-center">
    <!-- Video Background -->
    <video
      autoplay
      muted
      loop
      playsinline
      class="absolute inset-0 w-full h-full object-cover"
    >
      <source :src="videoUrl" type="video/mp4">
    </video>

    <!-- Dark overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-black/70 via-black/50 to-black/70" />

    <!-- Content -->
    <div class="relative z-10 text-center px-4 max-w-5xl mx-auto">
      <div class="inline-flex items-center gap-2 px-4 py-2 mb-8 bg-white/10 backdrop-blur-md rounded-full border border-white/20">
        <span class="relative flex h-2 w-2">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75" />
          <span class="relative inline-flex rounded-full h-2 w-2 bg-red-500" />
        </span>
        <span class="text-white text-sm font-medium">Live Now</span>
      </div>

      <h1 class="text-5xl md:text-7xl lg:text-8xl font-bold text-white mb-8 tracking-tight">
        Experience the
        <span class="relative inline-block">
          Future
          <svg class="absolute -bottom-2 left-0 w-full" viewBox="0 0 200 12" fill="none">
            <path d="M2 10C50 2 150 2 198 10" stroke="url(#gradient)" stroke-width="4" stroke-linecap="round" />
            <defs>
              <linearGradient id="gradient" x1="0" y1="0" x2="200" y2="0">
                <stop offset="0%" stop-color="#f472b6" />
                <stop offset="100%" stop-color="#c084fc" />
              </linearGradient>
            </defs>
          </svg>
        </span>
      </h1>

      <p class="text-xl md:text-2xl text-white/90 mb-12 max-w-3xl mx-auto font-light">
        Immerse yourself in breathtaking experiences that push the boundaries of what's possible.
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <UButton
          size="xl"
          class="bg-white text-gray-900 hover:bg-gray-100 px-10"
        >
          <UIcon name="i-lucide-play" class="mr-2" />
          Watch Now
        </UButton>

        <UButton
          size="xl"
          variant="outline"
          class="border-white/50 text-white hover:bg-white/10 px-10"
        >
          Explore More
        </UButton>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 z-10">
      <div class="flex flex-col items-center gap-2 text-white/60">
        <span class="text-xs uppercase tracking-widest">Scroll</span>
        <div class="w-6 h-10 border-2 border-white/30 rounded-full p-1">
          <div class="w-1.5 h-1.5 bg-white rounded-full animate-scroll-indicator mx-auto" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes scroll-indicator {
  0%, 100% {
    transform: translateY(0);
    opacity: 1;
  }
  50% {
    transform: translateY(16px);
    opacity: 0.3;
  }
}

.animate-scroll-indicator {
  animation: scroll-indicator 2s ease-in-out infinite;
}
</style>
