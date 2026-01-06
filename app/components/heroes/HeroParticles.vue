<script setup lang="ts">
// Hero 6: Interactive Particles
// Canvas-based particle system with mouse interaction
// Particles connect to nearby particles and respond to cursor movement
// Features varied colors, sizes, and smooth physics-based cursor interaction

import { ref, onMounted, onUnmounted } from 'vue'

interface Particle {
  x: number
  y: number
  vx: number
  vy: number
  radius: number
  baseRadius: number
  color: { r: number; g: number; b: number }
  opacity: number
  pulseSpeed: number
  pulseOffset: number
}

// Color palette for particles - indigo to cyan to violet spectrum
const colorPalette = [
  { r: 99, g: 102, b: 241 },   // indigo-500
  { r: 129, g: 140, b: 248 },  // indigo-400
  { r: 79, g: 70, b: 229 },    // indigo-600
  { r: 139, g: 92, b: 246 },   // violet-500
  { r: 6, g: 182, b: 212 },    // cyan-500
  { r: 34, g: 211, b: 238 },   // cyan-400
  { r: 167, g: 139, b: 250 },  // violet-400
]

const canvasRef = ref<HTMLCanvasElement | null>(null)
const mousePos = ref({ x: -1000, y: -1000 }) // Start off-screen
const targetMousePos = ref({ x: -1000, y: -1000 })
let particles: Particle[] = []
let animationId: number
let time = 0

const createParticles = (width: number, height: number) => {
  const count = Math.floor((width * height) / 12000)
  particles = Array.from({ length: Math.min(count, 120) }, () => {
    const baseRadius = Math.random() * 2.5 + 0.8
    return {
      x: Math.random() * width,
      y: Math.random() * height,
      vx: (Math.random() - 0.5) * 0.4,
      vy: (Math.random() - 0.5) * 0.4,
      radius: baseRadius,
      baseRadius,
      color: colorPalette[Math.floor(Math.random() * colorPalette.length)],
      opacity: Math.random() * 0.4 + 0.4,
      pulseSpeed: Math.random() * 0.02 + 0.01,
      pulseOffset: Math.random() * Math.PI * 2
    }
  })
}

const lerp = (start: number, end: number, factor: number) => {
  return start + (end - start) * factor
}

const animate = () => {
  const canvas = canvasRef.value
  if (!canvas) return

  const ctx = canvas.getContext('2d')
  if (!ctx) return

  time += 0.016 // ~60fps time increment

  // Smooth mouse position interpolation for fluid cursor following
  mousePos.value.x = lerp(mousePos.value.x, targetMousePos.value.x, 0.08)
  mousePos.value.y = lerp(mousePos.value.y, targetMousePos.value.y, 0.08)

  ctx.clearRect(0, 0, canvas.width, canvas.height)

  particles.forEach((p, i) => {
    // Gentle pulsing effect on radius
    const pulse = Math.sin(time * p.pulseSpeed * 60 + p.pulseOffset) * 0.3 + 1
    p.radius = p.baseRadius * pulse

    // Move particle with slight damping
    p.x += p.vx
    p.y += p.vy

    // Soft edge bouncing with velocity dampening
    if (p.x < 0) { p.x = 0; p.vx *= -0.8 }
    if (p.x > canvas.width) { p.x = canvas.width; p.vx *= -0.8 }
    if (p.y < 0) { p.y = 0; p.vy *= -0.8 }
    if (p.y > canvas.height) { p.y = canvas.height; p.vy *= -0.8 }

    // Smooth mouse interaction with falloff curve
    const dx = mousePos.value.x - p.x
    const dy = mousePos.value.y - p.y
    const distSq = dx * dx + dy * dy
    const dist = Math.sqrt(distSq)
    const interactionRadius = 180

    if (dist < interactionRadius && dist > 0) {
      // Smooth falloff using inverse square with dampening
      const force = Math.pow(1 - dist / interactionRadius, 2) * 0.8
      const angle = Math.atan2(dy, dx)
      
      // Apply repulsion force gradually
      p.vx -= Math.cos(angle) * force * 0.5
      p.vy -= Math.sin(angle) * force * 0.5
    }

    // Apply subtle friction to prevent particles from flying too fast
    p.vx *= 0.98
    p.vy *= 0.98

    // Clamp velocity
    const maxSpeed = 3
    const speed = Math.sqrt(p.vx * p.vx + p.vy * p.vy)
    if (speed > maxSpeed) {
      p.vx = (p.vx / speed) * maxSpeed
      p.vy = (p.vy / speed) * maxSpeed
    }

    // Draw particle with glow effect
    const gradient = ctx.createRadialGradient(p.x, p.y, 0, p.x, p.y, p.radius * 2)
    gradient.addColorStop(0, `rgba(${p.color.r}, ${p.color.g}, ${p.color.b}, ${p.opacity})`)
    gradient.addColorStop(0.5, `rgba(${p.color.r}, ${p.color.g}, ${p.color.b}, ${p.opacity * 0.5})`)
    gradient.addColorStop(1, `rgba(${p.color.r}, ${p.color.g}, ${p.color.b}, 0)`)
    
    ctx.beginPath()
    ctx.arc(p.x, p.y, p.radius * 2, 0, Math.PI * 2)
    ctx.fillStyle = gradient
    ctx.fill()

    // Core of particle
    ctx.beginPath()
    ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(${p.color.r}, ${p.color.g}, ${p.color.b}, ${p.opacity})`
    ctx.fill()

    // Connect nearby particles with gradient lines
    particles.slice(i + 1).forEach(p2 => {
      const dx2 = p.x - p2.x
      const dy2 = p.y - p2.y
      const dist2 = Math.sqrt(dx2 * dx2 + dy2 * dy2)

      if (dist2 < 130) {
        const lineOpacity = (1 - dist2 / 130) * 0.25
        
        // Create gradient line between particles
        const lineGradient = ctx.createLinearGradient(p.x, p.y, p2.x, p2.y)
        lineGradient.addColorStop(0, `rgba(${p.color.r}, ${p.color.g}, ${p.color.b}, ${lineOpacity})`)
        lineGradient.addColorStop(1, `rgba(${p2.color.r}, ${p2.color.g}, ${p2.color.b}, ${lineOpacity})`)
        
        ctx.beginPath()
        ctx.moveTo(p.x, p.y)
        ctx.lineTo(p2.x, p2.y)
        ctx.strokeStyle = lineGradient
        ctx.lineWidth = 0.5 + (1 - dist2 / 130) * 0.5
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
  targetMousePos.value = { x: e.clientX, y: e.clientY }
}

const handleMouseLeave = () => {
  targetMousePos.value = { x: -1000, y: -1000 }
}

onMounted(() => {
  handleResize()
  animate()
  window.addEventListener('resize', handleResize)
  window.addEventListener('mousemove', handleMouseMove)
  window.addEventListener('mouseleave', handleMouseLeave)
})

onUnmounted(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', handleResize)
  window.removeEventListener('mousemove', handleMouseMove)
  window.removeEventListener('mouseleave', handleMouseLeave)
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
