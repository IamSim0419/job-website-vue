<script setup>
import { useRouter } from 'vue-router'
import { reactive } from 'vue'
import { useToast } from 'vue-toastification'
import axios from 'axios'

const form = reactive({
  type: 'Full-Time',
  title: '',
  description: '',
  salary: '',
  location: '',
  company: {
    name: '',
    description: '',
    contactEmail: '',
    contactPhone: '',
  },
})

const router = useRouter()
const toast = useToast()

const handleSubmit = async () => {
  const newJob = {
    title: form.title,
    type: form.type,
    location: form.location,
    description: form.description,
    salary: form.salary,
    company: {
      name: form.company.name,
      description: form.company.description,
      contactEmail: form.company.contactEmail,
      contactPhone: form.company.contactPhone,
    },
  }

  try {
    const response = await axios.post('/api/jobs', newJob)
    toast.success('Job Added Successfully')
    router.push(`/job/${response.data.id}`)
  } catch (error) {
    console.error('Error fetching job', error)
    toast.error('Job Was Not Added')
  }
}
</script>

<template>
  <section>
    <div class="form-container">
      <div class="form-layout">
        <form @submit.prevent="handleSubmit">
          <h2 class="form-title">Add Job</h2>

          <!-- Job Type -->
          <div class="job-type">
            <label for="type" class="job-type-label">Job Type</label>
            <select v-model="form.type" id="type" name="type" class="job-type-select" required>
              <option value="Full-Time">Full-Time</option>
              <option value="Part-Time">Part-Time</option>
              <option value="Remote">Remote</option>
              <option value="Internship">Internship</option>
            </select>
          </div>

          <!-- Job Title -->
          <div class="job-title">
            <label class="job-title-label">Job Listing Name</label>
            <input
              v-model="form.title"
              type="text"
              id="name"
              name="name"
              class="job-title-input"
              placeholder="eg. Beautiful Apartment In Miami"
              required
            />
          </div>

          <!-- Job description -->
          <div class="job-desc">
            <label for="description" class="job-desc-label">Description</label>
            <textarea
              v-model="form.description"
              id="description"
              name="description"
              class="job-desc-textarea"
              rows="4"
              placeholder="Add any job duties, expectations, requirements, etc"
            ></textarea>
          </div>

          <!-- Job Salary -->
          <div class="job-salary">
            <label for="type" class="job-salary-label">Salary</label>
            <select
              v-model="form.salary"
              id="salary"
              name="salary"
              class="job-salary-select"
              required
            >
              <option value="Under $50K">under $50K</option>
              <option value="$50K - $60K">$50 - $60K</option>
              <option value="$60K - $70K">$60 - $70K</option>
              <option value="$70K - $80K">$70 - $80K</option>
              <option value="$80K - $90K">$80 - $90K</option>
              <option value="$90K - $100K">$90 - $100K</option>
              <option value="$100K - $125K">$100 - $125K</option>
              <option value="$125K - $150K">$125 - $150K</option>
              <option value="$150K - $175K">$150 - $175K</option>
              <option value="$175K - $200K">$175 - $200K</option>
              <option value="Over $200K">Over $200K</option>
            </select>
          </div>

          <!-- Job-location -->
          <div class="job-location">
            <label class="job-location-label"> Location </label>
            <input
              v-model="form.location"
              type="text"
              id="location"
              name="location"
              class="job-location-input"
              placeholder="Company Location"
              required
            />
          </div>

          <!-- Form company Information -->
          <h3 class="form-company-info">Company Info</h3>

          <div class="company-name">
            <label for="company" class="company-name-label">Company Name</label>
            <input
              v-model="form.company.name"
              type="text"
              id="company"
              name="company"
              class="company-name-input"
              placeholder="Company Name"
            />
          </div>

          <!-- Company Description -->
          <div class="company-desc">
            <label for="company_description" class="company-desc-label">Company Description</label>
            <textarea
              v-model="form.company.description"
              id="company_description"
              name="company_description"
              class="company-desc-textarea"
              rows="4"
              placeholder="What does your company do?"
            ></textarea>
          </div>

          <!-- Contact Email -->
          <div class="contact-email">
            <label for="contact_email" class="contact-email-label">Contact Email</label>
            <input
              v-model="form.company.contactEmail"
              type="email"
              id="contact_email"
              name="contact_email"
              class="contact-email-input"
              placeholder="Email address for applicants"
              required
            />
          </div>

          <!-- Contact Phone Number -->
          <div class="contact-phone">
            <label for="contact_phone" class="contact-phone-label">Contact Phone</label>
            <input
              v-model="form.company.contactPhone"
              type="tel"
              id="contact_phone"
              name="contact_phone"
              class="contact-phone-input"
              placeholder="Optional phone for applicants"
            />
          </div>

          <div>
            <button class="form-btn" type="submit">Add Job</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
@reference 'tailwindcss';

section {
  @apply bg-blue-50;
}

section .form-container {
  @apply max-w-7xl m-auto py-24 px-4;
}

.form-container .form-layout {
  @apply max-w-2xl mx-auto bg-white px-6 py-8 mb-4 shadow-md rounded-md border border-blue-800;
}

.form-layout .form-title {
  @apply text-3xl text-blue-800 text-center font-semibold mb-6;
}

.job-type {
  @apply mb-4;
}

.job-type-label {
  @apply block text-blue-800 font-bold mb-2;
}

.job-type-select {
  @apply border rounded w-full py-2 px-3;
}

.job-title {
  @apply mb-4;
}

.job-title-label {
  @apply block text-blue-800 font-bold mb-2;
}

.job-title-input {
  @apply border rounded w-full py-2 px-3 mb-2;
}

.job-desc {
  @apply mb-4;
}

.job-desc-label {
  @apply block text-blue-800 font-bold mb-2;
}

.job-desc-textarea {
  @apply border rounded w-full py-2 px-3;
}

.job-salary {
  @apply mb-4;
}

.job-salary-label {
  @apply block text-blue-800 font-bold mb-2;
}

.job-salary-select {
  @apply border rounded w-full py-2 px-3;
}

.job-location {
  @apply mb-4;
}

.job-location-label {
  @apply block text-blue-800 font-bold mb-2;
}

.job-location-input {
  @apply border rounded w-full py-2 px-3 mb-2;
}

.form-layout .form-company-info {
  @apply text-2xl mb-5;
}

.company-name {
  @apply mb-4;
}

.company-name-label {
  @apply block text-blue-800 font-bold mb-2;
}

.company-name-input {
  @apply border rounded w-full py-2 px-3;
}

.company-desc {
  @apply mb-4;
}

.company-desc-label {
  @apply block text-blue-800 font-bold mb-2;
}

.company-desc-textarea {
  @apply border rounded w-full py-2 px-3;
}

.contact-email {
  @apply mb-4;
}

.contact-email-label {
  @apply block text-blue-800 font-bold mb-2;
}

.contact-email-input {
  @apply border rounded w-full py-2 px-3;
}

.contact-phone {
  @apply mb-4;
}

.contact-phone-label {
  @apply block text-blue-800 font-bold mb-2;
}

.contact-phone-input {
  @apply border rounded w-full py-2 px-3;
}

.form-layout .form-btn {
  @apply bg-blue-800 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-sm w-full focus:outline-none;
}
</style>
