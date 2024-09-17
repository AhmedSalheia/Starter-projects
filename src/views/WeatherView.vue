<template>
  <BackArrow />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link
    href="https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap"
    rel="stylesheet"
  />

  <div
    :class="{
      'no-app w-[100%] md:w-[60%] lg:w-[40%] xl:w-[30%]': true,
      warm: weather.main !== undefined && weather.main.temp > 16
    }"
  >
    <main>
      <div class="search-box w-[100%] mb-5">
        <input
          type="text"
          class="search-bar black w-[100%] p-[15px] text-[#313131] text-2xl"
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="weather.main !== undefined">
        <div class="location-box">
          <div class="location text-white text-4xl text-center font-bold">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date text-white text-xl text-center italic">{{ buildDate() }}</div>
        </div>
        <div class="weather-box text-center">
          <div class="temp inline-block font-[900] text-white">
            {{ Math.round(weather.main.temp) }}℃
          </div>
          <div class="weather text-white text-[48px] font-bold italic">
            {{ weather.weather[0].main }}
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import BackArrow from '@/components/BackArrow.vue'
import { ref } from 'vue'

const API_KEY = 'e4cb5975e4ef71178816120c04713ff1'
const url_base = 'https://api.openweathermap.org/data/2.5/'
const query = ref('')
const weather = ref('')

function fetchWeather(e) {
  if (e.key == 'Enter') {
    fetch(`${url_base}weather?q=${query.value}&units=metric&APPID=${API_KEY}`)
      .then((res) => res.json())
      .then(setResults)
  }
}
function setResults(results) {
  weather.value = results
}

function buildDate() {
  let now = new Date()

  let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']
  let months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']

  return `${days[now.getDay()]} ${now.getDate()} ${months[now.getMonth()]} ${now.getFullYear()}`
}
</script>

<style>
#app:has(.no-app) {
  display: flex;
  justify-content: center;
}
div.no-app {
  background-image: url('@/assets/images/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;

  font-family: 'montserrat', sans-serif;
}
div.no-app.warm {
  background-image: url('@/assets/images/warm-bg.jpg');
}

div.no-app main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box .search-bar {
  appearance: none;
  background: none;
  border: none;
  outline: none;

  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0 16px 0 16px;

  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0 16px 0;

  transition: 0.4s;
}

.location-box .location {
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.weather-box .temp {
  font-size: 102px;
  padding: 10px 25px;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
