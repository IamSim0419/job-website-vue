<script setup>
import logo from '@/assets/images/logo.svg'
import { RouterLink, useRoute } from 'vue-router'

const isActiveLink = (routePath) => {
  const route = useRoute()
  return route.path === routePath
}

const navLinks = [
  { name: 'Home', path: '/' },
  { name: 'Jobs', path: '/jobs' },
  { name: 'Add Job', path: '/job/add' },
]
</script>

<template>
  <header>
    <div class="header-container">
      <RouterLink to="/" class="logo">
        <img :src="logo" alt="Logo" />
        <span class="text-lg font-bold">JobSpots</span>
      </RouterLink>

      <nav>
        <ul>
          <li v-for="link in navLinks" :key="link.name">
            <RouterLink
              :to="link.path"
              class="nav-links"
              :class="[
                isActiveLink(link.path)
                  ? 'border-b-4 border-b-blue-700 pb-[1px]'
                  : 'border-b-transparent',
              ]"
            >
              {{ link.name }}
            </RouterLink>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<style scoped>
@reference "tailwindcss";

header {
  @apply p-4 bg-gray-800 w-full text-white drop-shadow-gray-600 drop-shadow-md;
}

header .header-container {
  @apply flex items-center justify-between max-w-7xl mx-auto;
}

header img {
  @apply h-8 w-8 mr-0.5 m-0;
}

header ul {
  @apply flex gap-2 md:gap-4;
}

.header-container .logo {
  @apply flex items-center;
}

.header-container .nav-links {
  @apply flex items-center;
}

header ul {
  @apply flex space-x-3;
}
</style>
