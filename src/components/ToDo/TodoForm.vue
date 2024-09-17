<template>
  <form class="flex flex-col" @submit.prevent="submit">
    <input
      class="bg-zinc-500 text-white p-2 w-[100%] mb-3"
      type="text"
      placeholder="New ToDo Item"
      v-model="newToDo"
    />
    <button class="green" type="submit">Submit</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const emits = defineEmits(['submit'])

const newToDo = ref('')

function submit() {
  emits('submit', newToDo.value)

  newToDo.value = ''
}
</script>

<style scoped></style>
