<template>
  <div class="g-co-1 flex flex-col justify-evenly w-[80vw] lg:w-[50vw]">
    <BackArrow />
    <TodoForm @submit="(e) => todos.push({ title: e, done: false })" />

    <div>
      <div class="relative h-10 p-2 border-b-2 border-green-700 text-white">
        <input
          type="checkbox"
          @click="(e) => todos.forEach((td) => (td.done = e.target.checked))"
          :checked="todos.length !== 0 && todos.filter((e) => e.done).length === todos.length"
        />
        <span class="ms-1">Mark All As Done</span>
      </div>
      <ul class="w-[100%] h-[50vh] overflow-y-scroll overflow-x-hidden">
        <li v-for="todo in sort()" :key="todo.title">
          <to-do
            :todo="todo"
            @change="(e) => (todo.done = e)"
            @delete="(e) => (todos = todos.filter((td) => td !== e))"
          ></to-do>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import TodoForm from '@/components/ToDo/TodoForm.vue'
import ToDo from '@/components/ToDo/ToDo.vue'
import BackArrow from '@/components/BackArrow.vue'
import { ref } from 'vue'

const todos = ref([])

function sort() {
  let arr = [...todos.value]

  let falseArr = arr.filter((el) => el.done == false).reduce((acc, item) => [item, ...acc], [])
  let trueArr = arr.filter((el) => el.done == true).reduce((acc, item) => [item, ...acc], [])

  return [...falseArr, ...trueArr]
}
</script>

<style scoped></style>
