<script setup>
import { ref, computed } from 'vue'
import { RouterLink } from 'vue-router'

const props = defineProps({
  job: Object,
})

const showFullDescription = ref(false)

function toogleFullDescription() {
  showFullDescription.value = !showFullDescription.value
}

const truncatedDescription = computed(() => {
  let description = props.job.description // access description
  if (!showFullDescription.value) {
    // Updated the descriptions
    description = description.substring(0, 90) + '...'
  }
  return description
})
</script>

<template>
  <div class="job-card">
    <div class="card-container">
      <div class="card-meta">
        <div class="card-type">{{ job.type }}</div>
        <h3>{{ job.title }}</h3>
      </div>

      <div class="card-desc">
        <span>
          {{ truncatedDescription }}
        </span>
        <span @click="toogleFullDescription" class="toggle-desc">
          {{ showFullDescription ? ' Less' : ' More' }}
        </span>
      </div>

      <div class="card-salary">{{ job.salary }}</div>

      <!-- <div class="card-divider"></div> -->

      <div class="card-controls">
        <div class="card-location">
          <p>
            <i class="pi pi-map-marker text-lg"></i>
            <span>{{ job.location }}</span>
          </p>
          <RouterLink :to="`/job/${job.id}`" class="card-btn">Read More</RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@reference 'tailwindcss';

.job-card {
  @apply bg-white rounded-sm shadow-md relative;
}

.card-container {
  @apply p-4 flex flex-col h-full;
}

.card-container .card-meta {
  @apply mb-6;
}

.card-container .card-type {
  @apply text-gray-600 my-2;
}

.card-container h3 {
  @apply text-xl font-bold;
}

.card-container .card-desc {
  @apply mb-5;
}

.card-desc .toggle-desc {
  @apply text-blue-800 hover:text-blue-700 mb-5 cursor-pointer;
}

.card-container .card-salary {
  @apply text-blue-500;
}

/* .card-divider {
  @apply border border-gray-100 mb-5 mt-auto;
} */

.card-location {
  @apply flex flex-col lg:flex-row justify-between mb-4 border-t border-gray-300 mt-8 pt-7;
}

.card-location p {
  @apply flex md:items-center gap-0.5 text-orange-700 text-sm;
}

.card-location .card-btn {
  @apply bg-blue-800 hover:bg-blue-700 text-white px-4 py-2 rounded-sm text-center text-sm;
}

.card-controls {
  @apply mt-auto;
}
</style>
