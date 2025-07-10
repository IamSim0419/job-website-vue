<script setup>
import { reactive, onMounted } from 'vue'
import JobList from '@/components/JobList.vue'
// import jobData from '@/jobs.json'
import { RouterLink } from 'vue-router'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import axios from 'axios'

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
})

const state = reactive({
  jobs: [],
  isLoading: true,
})

onMounted(async () => {
  try {
    await new Promise((resolve) => setTimeout(resolve, 500))
    const response = await axios.get('/api/jobs')
    state.jobs = response.data
  } catch (error) {
    console.log('Error Fetching Jobs', error)
  } finally {
    state.isLoading = false
  }
})
</script>

<template>
  <section>
    <div class="job-container">
      <h2>Browse Jobs</h2>
      <!-- Show loading spinner while loading is true -->
      <div v-if="state.isLoading" class="loading-spinner">
        <PulseLoader size="10px" />
      </div>

      <!-- Show jobs when loading done -->
      <div v-else class="job-grid">
        <JobList
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <div v-if="showButton" class="button">
    <RouterLink to="/jobs" class="">View All Jobs</RouterLink>
  </div>
</template>

<style scoped>
@reference 'tailwindcss';

section {
  @apply bg-blue-50 px-4 py-10;
}

.job-container {
  @apply max-w-7xl m-auto;
}

.job-container h2 {
  @apply text-3xl md:text-4xl font-bold text-blue-700 mb-10 text-center;
}

.loading-spinner {
  @apply text-center mt-50;
}

.job-container .job-grid {
  @apply grid grid-cols-1 md:grid-cols-3 gap-6;
}

div.button {
  @apply m-auto max-w-lg bg-white px-4 py-10;
}

div.button a {
  @apply block bg-black text-white text-center py-4 px-6 rounded-sm hover:bg-gray-800;
}
</style>
