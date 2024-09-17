<template>
  <RouterLink
    to="/"
    class="flex text-zinc-300 hover:text-[#00bd7e] fill-zinc-300 hover:fill-[#00bd7e] p-5 absolute top-10 left-[10%]"
  >
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" class="me-3">
      <path d="M20,20 L2,10 L20,2" />
    </svg>
    Back
  </RouterLink>
</template>

<script setup>
import { RouterLink } from 'vue-router'
</script>

<style scoped></style>
