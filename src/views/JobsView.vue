<script setup>
import JobListings from '@/components/JobListings.vue'
import RiseLoader from 'vue-spinner/src/RiseLoader.vue'
import { ref } from 'vue'

const limitLoad = ref(6)
const isLoading = ref(false)
const hasMore = ref(true) // track whether more items exist
const totalItems = 22 // replace with your actual total count

async function lazyLoadMore() {
  if (isLoading.value || !hasMore.value) return

  isLoading.value = true

  try {
    await new Promise((resolve) => setTimeout(resolve, 500))
    const fetchedCount = 4 // replace with your actual fetched result length
    limitLoad.value += fetchedCount

    // If again loaded fewer than expected or reached total, disable
    if (fetchedCount < 4 || limitLoad.value >= totalItems) {
      hasMore.value = false
    }
  } catch (err) {
    console.error('Load failed:', err)
  } finally {
    isLoading.value = false
  }
}
</script>

<template>
  <JobListings :limit="limitLoad" />

  <div class="lazy-btn">
    <button
      @click="lazyLoadMore"
      :disabled="isLoading || !hasMore"
      :class="{ toDisabled: !hasMore }"
      class="btn"
    >
      <span v-if="isLoading">
        <RiseLoader size="5px" color="blue" />
      </span>
      <span v-else-if="hasMore">Load More</span>
      <span v-else>No More Items</span>
    </button>
  </div>
</template>

<style scoped>
@reference 'tailwindcss';

.lazy-btn {
  @apply flex justify-center items-center py-10;
}

.btn {
  @apply bg-black text-white px-4 py-1 rounded-sm cursor-pointer;
}

.toDisabled {
  @apply bg-gray-600 cursor-auto;
}
</style>
