<script setup lang="ts">
// Hero 6: Interactive Particles
// Canvas-based particle system with mouse interaction
// Particles connect to nearby particles and respond to cursor movement

import { ref, onMounted, onUnmounted } from 'vue'

interface Particle {
  x: number
  y: number
  vx: number
  vy: number
  radius: number
}

const canvasRef = ref<HTMLCanvasElement | null>(null)
const mousePos = ref({ x: 0, y: 0 })
let particles: Particle[] = []
let animationId: number

const createParticles = (width: number, height: number) => {
  const count = Math.floor((width * height) / 15000)
  particles = Array.from({ length: Math.min(count, 100) }, () => ({
    x: Math.random() * width,
    y: Math.random() * height,
    vx: (Math.random() - 0.5) * 0.5,
    vy: (Math.random() - 0.5) * 0.5,
    radius: Math.random() * 2 + 1
  }))
}

const animate = () => {
  const canvas = canvasRef.value
  if (!canvas) return

  const ctx = canvas.getContext('2d')
  if (!ctx) return

  ctx.clearRect(0, 0, canvas.width, canvas.height)

  particles.forEach((p, i) => {
    // Move particle
    p.x += p.vx
    p.y += p.vy

    // Bounce off edges
    if (p.x < 0 || p.x > canvas.width) p.vx *= -1
    if (p.y < 0 || p.y > canvas.height) p.vy *= -1

    // Mouse interaction
    const dx = mousePos.value.x - p.x
    const dy = mousePos.value.y - p.y
    const dist = Math.sqrt(dx * dx + dy * dy)
    if (dist < 150) {
      p.x -= dx * 0.02
      p.y -= dy * 0.02
    }

    // Draw particle
    ctx.beginPath()
    ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2)
    ctx.fillStyle = 'rgba(99, 102, 241, 0.8)'
    ctx.fill()

    // Connect nearby particles
    particles.slice(i + 1).forEach(p2 => {
      const dx2 = p.x - p2.x
      const dy2 = p.y - p2.y
      const dist2 = Math.sqrt(dx2 * dx2 + dy2 * dy2)

      if (dist2 < 120) {
        ctx.beginPath()
        ctx.moveTo(p.x, p.y)
        ctx.lineTo(p2.x, p2.y)
        ctx.strokeStyle = `rgba(99, 102, 241, ${0.3 - dist2 / 400})`
        ctx.stroke()
      }
    })
  })

  animationId = requestAnimationFrame(animate)
}

const handleResize = () => {
  const canvas = canvasRef.value
  if (!canvas) return

  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  createParticles(canvas.width, canvas.height)
}

const handleMouseMove = (e: MouseEvent) => {
  mousePos.value = { x: e.clientX, y: e.clientY }
}

onMounted(() => {
  handleResize()
  animate()
  window.addEventListener('resize', handleResize)
  window.addEventListener('mousemove', handleMouseMove)
})

onUnmounted(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', handleResize)
  window.removeEventListener('mousemove', handleMouseMove)
})
</script>

<template>
  <section class="relative min-h-screen bg-gray-950 flex items-center justify-center overflow-hidden">
    <!-- Canvas for particles -->
    <canvas ref="canvasRef" class="absolute inset-0" />

    <!-- Gradient overlay -->
    <div class="absolute inset-0 bg-gradient-to-b from-transparent via-gray-950/50 to-gray-950" />

    <!-- Content -->
    <div class="relative z-10 text-center px-4 max-w-4xl">
      <div class="inline-flex items-center gap-2 mb-6 px-4 py-2 bg-indigo-500/10 border border-indigo-500/20 rounded-full">
        <div class="w-2 h-2 bg-indigo-500 rounded-full animate-pulse" />
        <span class="text-indigo-400 text-sm font-medium">Interactive Experience</span>
      </div>

      <h1 class="text-5xl md:text-7xl font-bold text-white mb-6">
        Connect with
        <span class="text-indigo-400">Technology</span>
      </h1>

      <p class="text-xl text-gray-400 mb-10 max-w-2xl mx-auto">
        Move your cursor to interact with the particles. Watch how technology responds to human touch.
      </p>

      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <UButton
          size="xl"
          class="bg-indigo-600 hover:bg-indigo-700 px-8"
        >
          <UIcon name="i-lucide-zap" class="mr-2" />
          Experience It
        </UButton>

        <UButton
          size="xl"
          variant="ghost"
          color="white"
          class="px-8"
        >
          Learn How It Works
        </UButton>
      </div>

      <!-- Feature highlights -->
      <div class="mt-16 grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="p-6 bg-white/5 backdrop-blur-sm rounded-xl border border-white/10">
          <UIcon name="i-lucide-cpu" class="w-8 h-8 text-indigo-400 mb-4" />
          <h3 class="text-lg font-semibold text-white mb-2">Real-time Processing</h3>
          <p class="text-sm text-gray-400">60fps rendering with optimized canvas animations</p>
        </div>

        <div class="p-6 bg-white/5 backdrop-blur-sm rounded-xl border border-white/10">
          <UIcon name="i-lucide-mouse-pointer" class="w-8 h-8 text-indigo-400 mb-4" />
          <h3 class="text-lg font-semibold text-white mb-2">Interactive</h3>
          <p class="text-sm text-gray-400">Particles respond dynamically to cursor movement</p>
        </div>

        <div class="p-6 bg-white/5 backdrop-blur-sm rounded-xl border border-white/10">
          <UIcon name="i-lucide-network" class="w-8 h-8 text-indigo-400 mb-4" />
          <h3 class="text-lg font-semibold text-white mb-2">Connected</h3>
          <p class="text-sm text-gray-400">Particles form dynamic networks based on proximity</p>
        </div>
      </div>
    </div>
  </section>
</template>
