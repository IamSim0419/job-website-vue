<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <section class="notfound-section">
    <i class="pi pi-exclamation-triangle notfound-icon"></i>
    <h1 class="notfound-title">404 Not Found</h1>
    <p class="notfound-message">This page does not exist</p>
    <RouterLink to="/" class="notfound-link"> Go Back </RouterLink>
  </section>
</template>

<style scoped>
@reference 'tailwindcss';

.notfound-section {
  @apply flex flex-col justify-center items-center h-96 text-center;
}
.notfound-icon {
  @apply text-7xl text-yellow-500 mb-5;
}
.notfound-title {
  @apply text-5xl font-bold mb-4;
}
.notfound-message {
  @apply text-xl mb-5;
}
.notfound-link {
  @apply text-white bg-blue-800 rounded-md px-3 py-2 mt-4 no-underline transition-colors duration-200;
}
.notfound-link:hover {
  @apply bg-blue-700;
}
</style>
