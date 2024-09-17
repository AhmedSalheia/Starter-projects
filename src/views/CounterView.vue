<template>
  <div class="page g-co-1">
    <BackArrow />
    <Counter :end="date + ' ' + time"></Counter>

    <div
      class="absolute bottom-3 left-0 right-0 place-self-center flex lg:w-[50vw] w-[100vw] lg:flex-row flex-col"
    >
      <input
        class="mx-auto bg-zinc-500 text-white h-10 lg:mr-2 mb-3"
        type="date"
        style="width: 100%"
        :value="date"
        v-model="date"
      />

      <input
        class="mx-auto bg-zinc-500 text-white h-10 lg:ml-2 mb-3"
        type="time"
        style="width: 100%"
        :value="time"
        v-model="time"
      />
    </div>
  </div>
</template>

<script setup>
import Counter from '@/components/Counter/index.vue'
import BackArrow from '@/components/BackArrow.vue'
import { ref } from 'vue'

const date = ref('2025-01-25')
const time = ref('00:00:00')
</script>

<style scoped></style>
