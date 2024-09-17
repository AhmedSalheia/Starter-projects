<template>
  <div class="relative h-10 p-2 border-b-2 border-green-700 text-white bg-zinc-800">
    <input type="checkbox" @change="emits('change', !todo.done)" :checked="todo.done" />
    <span class="ms-5">{{ todo.title }}</span>

    <button
      class="btn text-red-600 fill-red-600 px-3 absolute right-0"
      @click="emits('delete', todo)"
    >
      <TrashCan />
    </button>
  </div>
</template>

<script setup>
import TrashCan from '../icons/TrashCan.vue'

defineProps({
  todo: {
    required: true,
    type: Object
  }
})

const emits = defineEmits(['change', 'delete'])
</script>

<style scoped>
div:has(input[type='checkbox'][checked]) {
  text-decoration: line-through;
  color: var(--color-text);
}
</style>
