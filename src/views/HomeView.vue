<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <div class="greetings">
        <h1 class="green">Hi There!!</h1>
        <h3>
          Those Are Some Apps and Components I've made Using
          <a href="https://vitejs.dev/" target="_blank" rel="noopener">Vite</a> And
          <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>. And The Help Of
          Some Youtube Videos. <br /><br />

          Ideas and Youtube Links are From:
          <a
            href="https://dev.to/nerdjfpb/15-vue-js-project-ideas-beginner-to-expert-with-tutorial-3ec2"
            target="_blank"
            rel="noopener"
          >
            This Article.
          </a>
        </h3>
      </div>
    </div>
  </header>

  <main>
    <WelcomeItem link="/counter">
      <template #icon>
        <icon-countdown />
      </template>
      <template #heading>Counter Component</template>

      A Countdown Component I Made With The Help Of
      <a href="https://www.youtube.com/watch?v=Q_fLx2KcoYA" target="_blank" rel="noopener"
        >This Youtube Video</a
      >. <br />
      It Takes an End Date And Starts Counting Down Till It's Reached. <br /><br />

      Props: <br />
      <a href="javascript:;">end</a>
      : A Valid Date String That Points The End Date Of The Timer.
    </WelcomeItem>

    <WelcomeItem link="/todo">
      <template #icon>
        <icon-todo />
      </template>
      <template #heading>ToDo List</template>

      A Todo List App Made With The Help of
      <a href="https://www.youtube.com/watch?v=-X2hP9pOVss" target="_blank" rel="noopener"
        >This Youtube Video</a
      >. <br />
      It Supports Add New, Delete Existing, Mark One As Done, Mark All As Done
    </WelcomeItem>

    <WelcomeItem link="/calculator">
      <template #icon>
        <icon-calculator />
      </template>
      <template #heading>Microsoft Standard Calculator (Win10)</template>

      A Calculator App Made With The Help of
      <a href="https://www.youtube.com/watch?v=m1_ih43p24s" target="_blank" rel="noopener"
        >This Youtube Video</a
      >. <br />
      It's Made Based On Windows10 Calculator (Standard) ... A Very Simpler Implimintation
    </WelcomeItem>

    <WelcomeItem link="/weather">
      <template #icon>
        <icon-weather />
      </template>
      <template #heading>Weather App</template>

      A Weather App Made With The Help of
      <a href="https://www.youtube.com/watch?v=JLc-hWsPTUY" target="_blank" rel="noopener"
        >This Youtube Video</a
      >. <br />
      It's Made With The Help Of
      <a href="https://openweatherapp.org" target="_blank">OpenWeatherApp API</a>.
    </WelcomeItem>
  </main>
</template>

<script setup>
import IconCountdown from '@/components/icons/IconCountdown.vue'
import IconTodo from '@/components/icons/IconTodo.vue'
import IconCalculator from '@/components/icons/IconCalculator.vue'
import IconWeather from '@/components/icons/IconWeather.vue'

import WelcomeItem from '@/components/WelcomeItem.vue'
</script>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
