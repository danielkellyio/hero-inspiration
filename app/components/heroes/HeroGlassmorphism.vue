<script setup lang="ts">
// Hero 7: Glassmorphism Design
// Modern glass-effect UI with blur, transparency, and depth
// Features layered glass cards with subtle shadows and borders
</script>

<template>
  <section class="relative min-h-screen overflow-hidden">
    <!-- Colorful background blobs -->
    <div class="absolute inset-0 bg-slate-900">
      <div
        class="absolute top-20 -left-20 w-96 h-96 bg-purple-500 rounded-full mix-blend-soft-light filter blur-3xl opacity-75 animate-blob"
      />
      <div
        class="absolute top-40 -right-20 w-96 h-96 bg-yellow-500 rounded-full mix-blend-soft-light filter blur-3xl opacity-75 animate-blob animation-delay-2000"
      />
      <div
        class="absolute -bottom-20 left-1/3 w-96 h-96 bg-pink-500 rounded-full mix-blend-soft-light filter blur-3xl opacity-75 animate-blob animation-delay-4000"
      />
      <div
        class="absolute bottom-40 right-1/4 w-80 h-80 bg-blue-500 rounded-full mix-blend-soft-light filter blur-3xl opacity-55 animate-blob animation-delay-3000"
      />
    </div>

    <!-- Content -->
    <div
      class="relative z-10 min-h-screen flex items-center justify-center px-4 py-20"
    >
      <div class="max-w-6xl mx-auto">
        <!-- Main glass card -->
        <div class="glass-card p-8 md:p-12 rounded-3xl">
          <div class="grid md:grid-cols-2 gap-12 items-center">
            <!-- Left content -->
            <div>
              <div
                class="inline-flex items-center gap-2 px-3 py-1.5 mb-6 bg-white/10 rounded-full"
              >
                <span class="w-2 h-2 bg-green-400 rounded-full" />
                <span class="text-white/80 text-sm">Available now</span>
              </div>

              <h1
                class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-6 leading-tight"
              >
                Beautiful
                <span
                  class="text-transparent bg-clip-text bg-gradient-to-r from-purple-400 to-pink-400"
                >
                  glass
                </span>
                interfaces
              </h1>

              <p class="text-lg text-white/70 mb-8 leading-relaxed">
                Create stunning visual effects with glassmorphism. Combine
                transparency, blur, and gradients for a modern, elegant look
                that captivates users.
              </p>

              <div class="flex flex-col sm:flex-row gap-4">
                <UButton size="xl" class="glass-button px-8">
                  <UIcon name="i-lucide-sparkles" class="mr-2" />
                  Try It Now
                </UButton>

                <UButton size="xl" variant="link" color="white" class="px-8">
                  View Examples
                  <template #trailing>
                    <UIcon name="i-lucide-external-link" />
                  </template>
                </UButton>
              </div>
            </div>

            <!-- Right - Hero image -->
            <div class="relative h-80 md:h-96 flex items-center justify-center">
              <div class="glass-image-frame rounded-3xl overflow-hidden">
                <img
                  src="~/assets/images/glassmorphism-person.png"
                  alt="Person working at computer"
                  class="w-full h-full object-cover rounded-2xl"
                />
              </div>
            </div>
          </div>
        </div>

        <!-- Bottom feature tags -->
        <div class="mt-8 flex flex-wrap justify-center gap-3">
          <span
            v-for="feature in [
              'Blur Effects',
              'Transparency',
              'Gradients',
              'Shadows',
              'Animations',
            ]"
            :key="feature"
            class="px-4 py-2 glass-tag rounded-full text-sm text-white/70"
          >
            {{ feature }}
          </span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.glass-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
}

.glass-card-small {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.2);
}

.glass-image-frame {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
  padding: 8px;
}

.glass-tag {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.glass-button {
  background: linear-gradient(
    135deg,
    rgba(168, 85, 247, 0.8),
    rgba(236, 72, 153, 0.8)
  );
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.glass-button:hover {
  background: linear-gradient(
    135deg,
    rgba(168, 85, 247, 0.9),
    rgba(236, 72, 153, 0.9)
  );
}

@keyframes blob {
  0%,
  100% {
    transform: translate(0, 0) scale(1);
  }
  25% {
    transform: translate(20px, -30px) scale(1.1);
  }
  50% {
    transform: translate(-20px, 20px) scale(0.9);
  }
  75% {
    transform: translate(30px, 10px) scale(1.05);
  }
}

.animate-blob {
  animation: blob 15s infinite ease-in-out;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-3000 {
  animation-delay: 3s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}
</style>
