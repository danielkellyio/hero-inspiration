<script setup lang="ts">
// Hero 8: Animated Gradient Mesh
// Complex gradient mesh background with organic shapes
// Creates a fluid, dynamic visual effect with smooth color transitions

const dashboardRef = ref<HTMLElement | null>(null)
const tiltStyle = ref({
  transform: 'perspective(1000px) rotateX(0deg) rotateY(0deg)'
})

function handleMouseMove(e: MouseEvent) {
  if (!dashboardRef.value) return

  const rect = dashboardRef.value.getBoundingClientRect()
  const centerX = rect.left + rect.width / 2
  const centerY = rect.top + rect.height / 2

  // Calculate rotation based on mouse position relative to center
  const rotateY = ((e.clientX - centerX) / (rect.width / 2)) * 8 // max 8 degrees
  const rotateX = ((centerY - e.clientY) / (rect.height / 2)) * 6 // max 6 degrees

  tiltStyle.value = {
    transform: `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`
  }
}

function handleMouseLeave() {
  tiltStyle.value = {
    transform: 'perspective(1000px) rotateX(0deg) rotateY(0deg)'
  }
}
</script>

<template>
  <section class="relative min-h-screen overflow-hidden bg-black">
    <!-- Animated mesh gradient background -->
    <div class="absolute inset-0">
      <!-- Base gradient -->
      <div
        class="absolute inset-0 bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900"
      />

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
    <div class="relative z-10 min-h-screen flex items-center">
      <div class="w-full max-w-7xl mx-auto px-6 lg:px-8 py-20">
        <div class="grid lg:grid-cols-2 gap-12 lg:gap-16 items-center">
          <!-- Left: Text content -->
          <div class="space-y-8">
            <!-- Eyebrow -->
            <div
              class="inline-flex items-center gap-2 px-4 py-2 bg-white/[0.08] backdrop-blur-md border border-white/[0.12] rounded-full"
            >
              <span class="w-2 h-2 bg-amber-400 rounded-full animate-pulse" />
              <span class="text-amber-200/90 text-sm font-medium tracking-wide">Enterprise Analytics Platform</span>
            </div>

            <!-- Main heading -->
            <h1
              class="hero-heading text-4xl sm:text-5xl lg:text-6xl font-semibold leading-[1.1] tracking-tight"
            >
              <span class="block text-white">Transform data into</span>
              <span class="block text-white relative uppercase">
                decisive action
                <svg
                  class="absolute -bottom-2 left-0 w-full h-3"
                  viewBox="0 0 300 12"
                  preserveAspectRatio="none"
                >
                  <path
                    d="M0,8 Q75,0 150,8 T300,8"
                    stroke="url(#underline-gradient)"
                    stroke-width="4"
                    fill="none"
                    stroke-linecap="round"
                  />
                  <defs>
                    <linearGradient
                      id="underline-gradient"
                      x1="0%"
                      y1="0%"
                      x2="100%"
                      y2="0%"
                    >
                      <stop
                        offset="0%"
                        stop-color="#a78bfa"
                      />
                      <stop
                        offset="50%"
                        stop-color="#f472b6"
                      />
                      <stop
                        offset="100%"
                        stop-color="#fb923c"
                      />
                    </linearGradient>
                  </defs>
                </svg>
              </span>
            </h1>

            <!-- Description -->
            <p
              class="text-lg lg:text-xl text-white/70 leading-relaxed max-w-xl"
            >
              Unify your business intelligence with real-time insights,
              predictive analytics, and automated reporting that scales with
              your organization.
            </p>

            <!-- CTAs -->
            <div class="flex flex-wrap items-center gap-4 pt-2">
              <UButton
                size="xl"
                class="mesh-button px-8"
              >
                Start Free Trial
                <template #trailing>
                  <UIcon name="i-lucide-arrow-right" />
                </template>
              </UButton>

              <UButton
                size="xl"
                variant="ghost"
                class="text-white/80 hover:text-white hover:bg-white/[0.06] px-6"
              >
                <UIcon
                  name="i-lucide-calendar"
                  class="mr-2 w-5 h-5"
                />
                Book a Demo
              </UButton>
            </div>

            <!-- Stats -->
            <div
              class="flex items-center gap-8 pt-6 border-t border-white/[0.08]"
            >
              <div>
                <div class="text-2xl lg:text-3xl font-semibold text-white">
                  2.4M+
                </div>
                <div class="text-sm text-white/50">
                  Active users
                </div>
              </div>
              <div class="w-px h-10 bg-white/[0.12]" />
              <div>
                <div class="text-2xl lg:text-3xl font-semibold text-white">
                  99.9%
                </div>
                <div class="text-sm text-white/50">
                  Uptime SLA
                </div>
              </div>
              <div class="w-px h-10 bg-white/[0.12]" />
              <div>
                <div class="text-2xl lg:text-3xl font-semibold text-white">
                  150+
                </div>
                <div class="text-sm text-white/50">
                  Integrations
                </div>
              </div>
            </div>
          </div>

          <!-- Right: Dashboard image with 3D tilt -->
          <div
            ref="dashboardRef"
            class="relative lg:pl-8 tilt-container"
            :style="tiltStyle"
            @mousemove="handleMouseMove"
            @mouseleave="handleMouseLeave"
          >
            <!-- Glow effect behind image -->
            <div
              class="absolute -inset-4 bg-gradient-to-r from-violet-500/20 via-fuchsia-500/20 to-amber-500/20 rounded-3xl blur-2xl opacity-60"
            />

            <!-- Dashboard mockup -->
            <div class="relative">
              <div
                class="dashboard-frame rounded-2xl overflow-hidden border border-white/[0.15] shadow-2xl"
              >
                <!-- Browser chrome -->
                <div
                  class="bg-slate-900/90 backdrop-blur-sm px-4 py-3 flex items-center gap-3 border-b border-white/[0.08]"
                >
                  <div class="flex gap-2">
                    <span class="w-3 h-3 rounded-full bg-red-500/80" />
                    <span class="w-3 h-3 rounded-full bg-yellow-500/80" />
                    <span class="w-3 h-3 rounded-full bg-green-500/80" />
                  </div>
                  <div class="flex-1 mx-4">
                    <div
                      class="bg-slate-800/80 rounded-lg px-4 py-1.5 text-sm text-white/40 max-w-xs"
                    >
                      app.analytics.io/dashboard
                    </div>
                  </div>
                </div>

                <!-- Dashboard content -->
                <div class="bg-slate-950/95 p-6">
                  <img
                    src="https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=800&h=500&fit=crop&auto=format"
                    alt="Analytics Dashboard"
                    class="w-full h-auto rounded-lg"
                  >
                </div>
              </div>

              <!-- Floating notification card - animates in then stays static -->
              <div
                class="absolute -left-6 bottom-24 card-pop-in bg-slate-900/95 backdrop-blur-md border border-white/[0.15] rounded-xl p-4 shadow-xl max-w-[200px]"
              >
                <div class="flex items-center gap-3">
                  <div
                    class="w-10 h-10 rounded-full bg-gradient-to-br from-emerald-400 to-cyan-400 flex items-center justify-center"
                  >
                    <UIcon
                      name="i-lucide-trending-up"
                      class="w-5 h-5 text-slate-900"
                    />
                  </div>
                  <div>
                    <div class="text-sm font-medium text-white">
                      Revenue up
                    </div>
                    <div class="text-emerald-400 text-lg font-semibold">
                      +24.5%
                    </div>
                  </div>
                </div>
              </div>

              <!-- Floating metric card - animates in then stays static -->
              <div
                class="absolute -right-4 top-20 card-pop-in-delayed bg-slate-900/95 backdrop-blur-md border border-white/[0.15] rounded-xl p-4 shadow-xl"
              >
                <div class="flex items-center gap-2 mb-2">
                  <span
                    class="w-2 h-2 rounded-full bg-amber-400 animate-pulse"
                  />
                  <span class="text-xs text-white/60 uppercase tracking-wider">Live</span>
                </div>
                <div class="text-2xl font-semibold text-white">
                  8,429
                </div>
                <div class="text-sm text-white/50">
                  Active sessions
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(50px, 30px) scale(1.1);
  }
  66% {
    transform: translate(-30px, 50px) scale(0.95);
  }
}

@keyframes mesh-float-2 {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(-40px, 40px) scale(0.9);
  }
  66% {
    transform: translate(30px, -30px) scale(1.05);
  }
}

@keyframes mesh-float-3 {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(60px, -40px) scale(1.15);
  }
  66% {
    transform: translate(-50px, 30px) scale(0.9);
  }
}

@keyframes mesh-float-4 {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(-30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(40px, 20px) scale(0.95);
  }
}

@keyframes mesh-float-5 {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, 60px) scale(0.85);
  }
  66% {
    transform: translate(-60px, -20px) scale(1.1);
  }
}

.hero-heading {
  text-shadow: 0 4px 30px rgba(0, 0, 0, 0.4);
}

.mesh-button {
  background: linear-gradient(135deg, #7c3aed, #a855f7);
  border: none;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(124, 58, 237, 0.4);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
}

.mesh-button:hover {
  box-shadow: 0 6px 30px rgba(124, 58, 237, 0.6);
  transform: translateY(-2px);
}

.mesh-button::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, #a855f7, #7c3aed);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.mesh-button:hover::before {
  opacity: 1;
}

.dashboard-frame {
  background: linear-gradient(
    135deg,
    rgba(30, 27, 75, 0.8),
    rgba(30, 27, 75, 0.6)
  );
  backdrop-filter: blur(10px);
}

.tilt-container {
  transition: transform 0.15s ease-out;
  transform-style: preserve-3d;
}

.card-pop-in {
  animation: popIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  animation-delay: 0.3s;
  opacity: 0;
  transform: scale(0.8);
}

.card-pop-in-delayed {
  animation: popIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  animation-delay: 0.5s;
  opacity: 0;
  transform: scale(0.8);
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: scale(0.8);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

.noise-bg {
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}
</style>
