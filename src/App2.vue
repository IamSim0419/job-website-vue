<script>
// Option API example for Vue.js
// This code defines a simple Vue.js application that displays job listings and allows users to apply for jobs.
// It uses the Vue.js Options API to manage state and methods.
export default {
  name: 'App',
  data() {
    return {
      message: 'Welcome to FindJobs!',
      status: 'active', // This can be 'active' or 'pending'/'inactive'
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
    }
  },

  methods: {
    applyForJob() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    },
  },
}
</script>

<template>
  <div>
    <h1>{{ message }}</h1>
    <p v-if="status === 'active'">Job listings are available!</p>
    <p v-else-if="status === 'pending'">Job listings are being processed.</p>
    <p v-else>No job listings available at the moment.</p>

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
</template>

<style scoped></style>
