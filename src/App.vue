<script setup>
import { ref } from 'vue'
import Button from './components/Button.vue'
import Score from './components/Score.vue'
import CardWord from './components/CardWord.vue'

const score = ref('100')
</script>

<template>
  <header class="header container">
    <div class="header-title">Запомни слово</div>
    <Score :count="score" />
  </header>
  <main class="main">
    <CardWord />
    <Button>Начать игру</Button>
  </main>
</template>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 35px;
}

.header-title {
  letter-spacing: 1.92px;
  font-weight: 700;
  color: var(--color-text-secondary);
  text-transform: uppercase;
}

.main {
  display: grid;
  place-items: center;
  min-height: 100vh;
}
</style>
