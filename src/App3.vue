<script setup>
// Composition API example for Vue.js
import { reactive, computed, onMounted, ref } from 'vue'

const state = reactive({
  name: 'Mio Imada',
  status: 'active',
  jobs: [
    { id: 1, title: 'Software Engineer', company: 'Tech Corp' },
    { id: 2, title: 'Data Scientist', company: 'Data Inc.' },
    { id: 3, title: 'Product Manager', company: 'Product Co.' },
  ],
  links: [
    { name: 'Home', url: '/' },
    { name: 'Jobs', url: '/jobs' },
    { name: 'Contact', url: '/contact' },
  ],

  newJob: {
    title: '',
    company: '',
  },
})

function applyForJob() {
  if (state.status === 'active') {
    state.status = 'pending'
  } else if (state.status === 'pending') {
    state.status = 'inactive'
  } else {
    state.status = 'active'
  }
}

// Using ref to create a reactive reference for todo items
const todoItems = ref([])

const addJob = () => {
  if (state.newJob.title.trim() !== '') {
    const newJob = {
      id: state.jobs.length + 1,
      title: state.newJob.title,
      company: state.newJob.company || 'Unknown Company',
    }

    // state.jobs.push(state.newJob) // this can use the same object reference
    // but we create a new object to avoid mutating the original state directly
    // This is a good practice to ensure reactivity and avoid side effects
    // in Vue's reactivity system.
    state.jobs.push(newJob)
    state.newJob = { title: '', company: '' } // Clear the input fields after adding the job
  }
}

const removeJob = (index) => {
  if (index >= 0 && index < state.jobs.length) {
    state.jobs.splice(index, 1) // Remove the job at the specified index
  }
}

// Computed properties for reactive state
// These properties will automatically update when the state/data changes
// computed refs are used to derive values from the reactive state
const name = computed(() => state.name)
const status = computed(() => state.status)
const jobs = computed(() => state.jobs)
const links = computed(() => state.links)
const newJob = computed({
  get: () => state.newJob,
  set: (value) => (state.newJob = value),
})

// This lifecycle hook runs when the component is mounted
onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await response.json()
    todoItems.value = data.slice(0, 10) // Limit to first 10 items for simplicity
    console.log('Todo items fetched:', todoItems.value)
  } catch (error) {
    console.error('Error fetching todo items:', error)
  }
})
</script>

<template>
  <div>
    <!-- used {{  name  }} in the template (Vue unwraps .value for you) -->
    <h1>{{ name }}</h1>
    <p v-if="status === 'active'">Job listings are available!</p>
    <p v-else-if="status === 'pending'">Job listings are being processed.</p>
    <p v-else>No job listings available at the moment.</p>

    <br />

    <!-- Form to add a new job listing -->
    <h2>Add a New Job Listing</h2>
    <form @submit.prevent="addJob">
      <label for="newJob">New Job:</label>
      <input type="text" id="newJob" v-model="newJob.title" />
      <label for="newCompany">Company:</label>
      <input type="text" id="newCompany" v-model="newJob.company" />
      <button type="submit">Add Job</button>
    </form>

    <!-- Displaying the list of jobs -->
    <h2>Current Job Listings</h2>
    <p v-for="(job, index) in state.jobs" :key="index">
      <span>{{ job.title }}</span> at
      <span>{{ job.company }}</span>
      <button @click="removeJob(index)">X</button>
    </p>
    <p v-if="jobs.length === 0">No job listings available.</p>

    <br />

    <!-- Available Job Listings -->
    <h3>Available Job Listings:</h3>
    <ul>
      <li v-for="job in jobs" :key="job.id">{{ job.title }} at {{ job.company }}</li>
    </ul>

    <nav>
      <ul>
        <li v-for="link in links" :key="link.name">
          <a :href="link.url">{{ link.name }}</a>
        </li>
      </ul>
    </nav>
  </div>

  <br />

  <button @click="applyForJob" style="cursor: pointer">Apply for Job</button>

  <h2>Todo Items</h2>
  <ul>
    <li v-for="item in todoItems" :key="item.id">
      {{ item.title }}
    </li>
  </ul>
</template>
<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 300px;
  background-color: rgb(218, 218, 218);
  padding: 18px 8px;
  color: black;
  border-radius: 10px;
}
</style>
