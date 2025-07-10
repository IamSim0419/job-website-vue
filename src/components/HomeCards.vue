<script setup>
import CardCom from './CardCom.vue'
import { RouterLink } from 'vue-router'
</script>

<template>
  <section>
    <div class="card-container">
      <div class="grid-card">
        <!-- Developer Card -->
        <CardCom bg="bg-violet-200">
          <h2 class="card-title">For Developers</h2>
          <p class="mt-2 mb-4">Browse our Vue jobs and start your career today</p>
          <RouterLink to="/jobs" class="card-link bg-black hover:bg-gray-900">
            Browse Jobs
          </RouterLink>
        </CardCom>

        <!-- Employer Card -->
        <CardCom>
          <h2 class="card-title">For Employers</h2>
          <p class="mt-2 mb-4">List your job to find the perfect developer for the role</p>
          <RouterLink to="/job/add" class="card-link bg-blue-800 hover:bg-blue-700">
            Add Job
          </RouterLink>
        </CardCom>
      </div>
    </div>
  </section>
</template>

<style scoped>
@reference 'tailwindcss';

section {
  @apply py-4;
}

section .card-container {
  @apply max-w-7xl m-auto;
}

.grid-card {
  @apply grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg;
}

.grid-card .card-title {
  @apply text-2xl font-bold;
}

.grid-card .card-link {
  @apply inline-block text-white rounded-md px-4 py-2 hover:shadow-sm hover:shadow-gray-600;
}
</style>
