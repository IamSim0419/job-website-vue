<script setup>
import HeroComp from '@/components/HeroComp.vue'
import HomeCards from '@/components/HomeCards.vue'
import JobListing from '@/components/JobListings.vue'
</script>

<template>
  <main>
    <HeroComp title="Become a Software Engineer" subtitle="Your Next Job Starts Here!" />
    <HomeCards />
    <JobListing :limit="3" :showButton="true" />
  </main>
</template>

<style scoped>
@reference 'tailwindcss';
</style>
