<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <section>
    <div class="max-w-7xl m-auto py-6 px-6">
      <RouterLink to="/jobs" class="text-blue-800 hover:text-blue-700 flex items-center">
        <i class="pi pi-arrow-circle-left mr-2"></i> Back to Job Listings
      </RouterLink>
    </div>
  </section>
</template>

<style scoped>
@reference 'tailwindcss';
</style>
