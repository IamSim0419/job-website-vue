<script setup>
defineProps({
  title: {
    type: String,
    default: 'Become a Vue Engineer',
  },
  subtitle: {
    String,
    default: 'Looking for a Job?',
  },
})
</script>

<template>
  <section class="hero">
    <div class="hero-container">
      <div class="hero-details">
        <h1>{{ title }}</h1>
        <p>{{ subtitle }}</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
@reference "tailwindcss";

section.hero {
  @apply bg-gray-950 py-20 mb-4;
}

section .hero-container {
  @apply max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col items-center;
}

.hero .hero-details {
  @apply text-center;
}

.hero h1 {
  @apply text-4xl font-extrabold text-white sm:text-5xl md:text-6xl;
}

.hero p {
  @apply my-4 text-xl text-white;
}
</style>
