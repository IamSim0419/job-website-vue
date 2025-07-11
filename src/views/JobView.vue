<script setup>
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import BackButton from '@/components/BackButton.vue'
import { reactive, onMounted } from 'vue'
import { useRoute, RouterLink, useRouter } from 'vue-router'
import { useToast } from 'vue-toastification'
import axios from 'axios'

const route = useRoute()
const router = useRouter()
const toast = useToast()

const jobId = route.params.id

const state = reactive({
  job: {},
  isLoading: true,
})

// const deleteJob = async () => {
//   try {
//     const confirm = window.confirm('Are you sure you want to delete this job?')
//     if (confirm) {
//       await axios.delete(`/api/jobs/${jobId}`)
//       toast.success('Job Deleted Successfully')
//       router.push('/jobs')
//     }
//   } catch (error) {
//     console.error('Error deleting job', error)
//     toast.error('Job Not Deleted')
//   }
// }

// onMounted(async () => {
//   try {
//     const response = await axios.get(`/api/jobs/${jobId}`)
//     state.job = response.data
//   } catch (error) {
//     console.error('Error fetching job', error)
//   } finally {
//     state.isLoading = false
//   }
// })

// Mock Fetching from public/jobs.json
onMounted(async () => {
  try {
    const response = await axios.get('/jobs.json') // read full file
    const jobs = response.data

    // Find specific job by id
    const job = jobs.find((job) => job.id == jobId)

    if (!job) {
      throw new Error('Job not found')
    }

    state.job = job
  } catch (error) {
    console.error('Error fetching job by ID', error)
    toast.error('Failed to load job details')
  } finally {
    state.isLoading = false
  }
})
</script>

<template>
  <!-- Back Button -->
  <BackButton />
  <section class="job-details-section">
    <div v-if="!state.isLoading" class="container">
      <div class="job-layout">
        <main>
          <div class="job-header">
            <div class="job-type">{{ state.job.type }}</div>
            <h1 class="job-title">{{ state.job.title }}</h1>
            <div class="job-location">
              <i class="pi pi-map-marker location-icon"></i>
              <p class="location-text">{{ state.job.location }}</p>
            </div>
          </div>

          <div class="job-description-box">
            <h3 class="section-title">Job Description</h3>
            <p class="section-paragraph">{{ state.job.description }}</p>
            <h3 class="section-title">Salary</h3>
            <p class="section-paragraph">{{ state.job.salary }}</p>
          </div>
        </main>

        <aside>
          <div class="company-info-box">
            <h3 class="aside-title">Company Info</h3>
            <h2 class="company-name">{{ state.job.company.name }}</h2>
            <p class="company-description">{{ state.job.company.description }}</p>
            <hr class="divider" />
            <h3 class="aside-title">Contact Email:</h3>
            <p class="contact">{{ state.job.company.contactEmail }}</p>
            <h3 class="aside-title">Contact Phone:</h3>
            <p class="contact">{{ state.job.company.contactPhone }}</p>
          </div>

          <div class="manage-box">
            <h3 class="aside-title">Manage Job</h3>
            <RouterLink :to="`/job/edit/${state.job.id}`" class="edit-button">
              Edit Job
            </RouterLink>
            <button @click="deleteJob" class="delete-button">Delete Job</button>
          </div>
        </aside>
      </div>
    </div>

    <div v-else class="loading-spinner">
      <PulseLoader size="12px" />
    </div>
  </section>
</template>

<style scoped>
@reference 'tailwindcss';

.job-details-section {
  @apply bg-blue-50;
}

.container {
  @apply max-w-7xl mx-auto py-10 px-4;
}

.job-layout {
  @apply grid grid-cols-1 md:grid-cols-[2fr_1fr] gap-6;
}

.job-header {
  @apply bg-white p-6 rounded-sm shadow-md text-center md:text-left;
}

.job-type {
  @apply text-gray-500 mb-4;
}

.job-title {
  @apply text-3xl font-bold mb-4;
}

.job-location {
  @apply text-gray-500 mb-4 flex items-center justify-center md:justify-start;
}

.location-icon {
  @apply text-lg text-orange-700 mr-2;
}

.location-text {
  @apply text-orange-700;
}

.job-description-box {
  @apply bg-white p-6 rounded-sm shadow-md mt-6;
}

.section-title {
  @apply text-green-800 text-lg font-bold mb-2;
}

.section-paragraph {
  @apply mb-4;
}

.company-info-box {
  @apply bg-white p-6 rounded-sm shadow-md;
}

.aside-title {
  @apply text-xl font-bold mb-6;
}

.company-name {
  @apply text-2xl;
}

.company-description {
  @apply my-2;
}

.divider {
  @apply my-4;
}

.contact {
  @apply my-2 bg-blue-100 p-2;
}

.manage-box {
  @apply bg-white p-6 rounded-lg shadow-sm mt-6;
}

.edit-button {
  @apply bg-blue-800 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-sm w-full focus:outline-none text-center  mt-4 block;
}

.delete-button {
  @apply bg-red-600 hover:bg-red-500 text-white font-bold py-2 px-4 rounded-sm w-full focus:outline-none mt-4 block cursor-pointer;
}

.loading-spinner {
  @apply text-center bg-white mt-60;
}
</style>
