<template>
  <section class="grid grid-cols-4 text-white relative">
    <div
      class="prev text-right text-zinc-500 col-span-full mb-3 text-xl pr-2 overflow-hidden w-[25rem]"
    >
      {{ prev }}
    </div>
    <div
      class="display text-right col-span-full mb-3 text-3xl pr-2 overflow-x-scroll overflow-y-hidden w-[25rem]"
    >
      {{ current || 0 }}
    </div>

    <button @click="percent" class="rounded mr-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      %
    </button>
    <button @click="clearCell" class="rounded mx-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      CE
    </button>
    <button @click="clearAll" class="rounded mx-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      C
    </button>
    <button @click="removeLast" class="rounded ml-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      remove last
    </button>

    <button @click="divX" class="rounded mr-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      <sup>1</sup>/<sub>x</sub>
    </button>
    <button @click="square" class="rounded mx-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      X<sup><small>2</small></sup>
    </button>
    <button @click="sqrt" class="rounded mx-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">
      sqrt
    </button>
    <button @click="div" class="rounded ml-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">÷</button>

    <button @click="num(7)" class="rounded mr-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      7
    </button>
    <button @click="num(8)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      8
    </button>
    <button @click="num(9)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      9
    </button>
    <button @click="mul" class="rounded ml-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">×</button>

    <button @click="num(4)" class="rounded mr-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      4
    </button>
    <button @click="num(5)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      5
    </button>
    <button @click="num(6)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      6
    </button>
    <button @click="min" class="rounded ml-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">-</button>

    <button @click="num(1)" class="rounded mr-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      1
    </button>
    <button @click="num(2)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      2
    </button>
    <button @click="num(3)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      3
    </button>
    <button @click="plus" class="rounded ml-[1px] my-[1px] bg-zinc-800 hover:bg-zinc-700">+</button>

    <button @click="sign" class="rounded mr-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      <sup> <b>+</b> </sup>/<sub><b>-</b></sub>
    </button>
    <button @click="num(0)" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">
      0
    </button>
    <button @click="dot" class="rounded mx-[1px] my-[1px] bg-zinc-700 hover:bg-zinc-800">.</button>
    <button
      @click="equal"
      class="rounded ml-[1px] my-[1px] bg-cyan-400 hover:bg-cyan-500 text-black"
    >
      =
    </button>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const prev = ref('')
const current = ref('')
const op = ref(null)
const equalPressed = ref(false)

const percent = () => (current.value = (parseFloat(current.value) / 100).toString())
const clearAll = () => {
  clearCell()
  prev.value = ''
}
const clearCell = () => (current.value = '')
const removeLast = () => {
  if (!equalPressed.value) current.value = current.value.slice(0, current.value.length - 1)
}

const divX = () => (current.value = (1 / parseFloat(current.value)).toString())
const square = () =>
  (current.value = (parseFloat(current.value) * parseFloat(current.value)).toString())

const sqrt = () => (current.value = Math.sqrt(parseFloat(current.value)))
const sign = () => (current.value = (parseFloat(current.value) * -1).toString())

const div = () => {
  if (op.value !== null) prev.value = equal(false)

  op.value = (a, b) => a / b
  prev.value = current.value
  current.value = ''
}
const mul = () => {
  if (op.value !== null) prev.value = equal(false)

  op.value = (a, b) => a * b
  prev.value = current.value
  current.value = ''
}
const plus = () => {
  if (op.value !== null) prev.value = equal(false)

  op.value = (a, b) => a + b
  prev.value = current.value
  current.value = ''
}
const min = () => {
  if (op.value !== null) prev.value = equal(false)

  op.value = (a, b) => a - b
  prev.value = current.value
  current.value = ''
}

const equal = (btnPressed = true) => {
  if (op.value !== null)
    current.value = op.value(parseFloat(prev.value), parseFloat(current.value || 0)).toString()

  op.value = null
  prev.value = ''

  if (btnPressed) equalPressed.value = true
}

const num = (n) => {
  if (equalPressed.value) {
    current.value = ''
    equalPressed.value = false
  }

  if (n == 0 && current.value == '') return

  current.value = `${current.value}${n}`
}
const dot = () => {
  if (equalPressed.value) {
    current.value = ''
    equalPressed.value = false
  }

  if (current.value.indexOf('.') === -1) {
    if (current.value == '') current.value = '0'

    num('.')
  }
}
</script>

<style scoped>
button {
  padding: 10px;
}
</style>
