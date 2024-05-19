<script setup>
import { ref } from 'vue'
import CurrentGPACalc from './components/CurrentGPACalc.vue'
import FutureGPACalc from './components/FutureGPACalc.vue'

const calculatorType = ref('current')
</script>

<template>
  <main>
    <div id="container">
      <button @click="calculatorType = 'current'" class="btn btn-primary btn-ghost" id="cGPA">
        Current GPA Calculator
      </button>
      <button @click="calculatorType = 'future'" class="btn btn-primary btn-ghost" id="fGPA">
        Future GPA Calculator
      </button>

      <div id="calculator">
        <CurrentGPACalc v-if="calculatorType === 'current'" />
        <FutureGPACalc v-else />
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
@import 'https://cdn.jsdelivr.net/gh/alphardex/aqua.css@master/dist/aqua.min.css';
</style>

<style scoped>
header {
  line-height: 1.5;
}

main {
  display: flex;
  justify-content: center;
  height: 100vh;
  margin: 0;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
}
@keyframes shake
{
  10%,
  90% {
    transform: translate3d(-2px, 0, 0);
  }

  40%,
  80% {
    transform: translate3d(1px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-2px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(2px, 0, 0);
  }
}

#container {
  width: 50rem;
  display: grid;
  grid-template-columns: repeat(autofill, minmax(300px, 1fr));
  grid-column-gap: 1rem;
}

#cGPA {
  grid-column-start: 1;
  margin: 1rem;
  max-height: 80px;
}

#fGPA {
  grid-column-start: 2;
  margin: 1rem;
  max-height: 80px;
}

#calculator {
  grid-column-start: 1;
  grid-column-end: 3;
}

.btn {
  padding: 8px 20px;
  border-radius: 20px;
  overflow: hidden;

  &::before {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(120deg, transparent, var(--primary-color), transparent);
    transform: translateX(-100%);
    transition: 0.6s;
  }
  &:hover {
    background: transparent;
    box-shadow: 0 0 20px 10px hsla(204, 70%, 53%, 0.5);
    animation: shake 0.82s both;
    &::before {
      transform: translateX(100%);
    }
  }
}
</style>
