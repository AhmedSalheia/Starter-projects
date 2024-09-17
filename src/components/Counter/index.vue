<template>
  <div v-on-mount>
    <div v-if="loaded">
      <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
        <span v-if="!expired">Buy Now!!</span>
        <span v-else>Timer Is Done</span>
      </section>
      <section class="flex text-6xl items-baseline content-center justify-center align-middle my-5">
        <div class="days flex mr-3 flex-col">
          <span>{{ formatNum(days) }}</span>
          <div class="label text-sm justify-self-center">Days</div>
        </div>
        <span class="leading-snug">:</span>

        <div class="hours flex mx-3 flex-col">
          <span>{{ formatNum(hours) }}</span>
          <div class="label text-sm bottom-0">Hours</div>
        </div>
        <span class="leading-snug">:</span>

        <div class="minutes flex mx-3 flex-col">
          <span>{{ formatNum(minutes) }}</span>
          <div class="label text-sm bottom-0">Minutes</div>
        </div>
        <span class="leading-snug">:</span>

        <div class="seconds flex ml-3 flex-col">
          <span>{{ formatNum(seconds) }}</span>
          <div class="label text-sm bottom-0">Seconds</div>
        </div>
      </section>

      <section class="text-xl mx-auto text-left">
        <span>Till: </span>
        <span class="text-white">{{ new Date(end).toLocaleString() }}</span>
      </section>
    </div>

    <div v-else>
      <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
        <span>Loading...</span>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const vOnMount = {
  mounted: () => {
    showRemaining()
  }
}

const props = defineProps({
  end: {
    required: true,
    type: String
  }
})

const days = ref(0)
const hours = ref(0)
const minutes = ref(0)
const seconds = ref(0)
const loaded = ref(false)
const expired = ref(false)

const _seconds = 1000
const _minutes = _seconds * 60
const _hours = _minutes * 60
const _days = _hours * 24

const formatNum = (num) => (num < 10 ? '0' + num : num)

function showRemaining() {
  setInterval(() => {
    const end = new Date(props.end).getTime()
    const distance = end - Date.now()

    if (distance < 0) {
      loaded.value = true
      expired.value = true

      days.value = 0
      hours.value = 0
      minutes.value = 0
      seconds.value = 0

      return
    }

    days.value = Math.floor(distance / _days)
    hours.value = Math.floor((distance % _days) / _hours)
    minutes.value = Math.floor((distance % _hours) / _minutes)
    seconds.value = Math.floor((distance % _minutes) / _seconds)

    loaded.value = true
  }, 1000)
}
</script>

<style scoped></style>
