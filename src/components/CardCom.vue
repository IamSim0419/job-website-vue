<script setup>
defineProps({
  bg: {
    type: String,
    default: 'bg-gray-300',
  },
})
</script>

<template>
  <div :class="`${bg} card`">
    <slot />
  </div>
</template>

<style scoped>
@reference 'tailwindcss';

.card {
  @apply p-6 rounded-sm hover:shadow-sm hover:shadow-gray-700 transition-shadow;
}
</style>
