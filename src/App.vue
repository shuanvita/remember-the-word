<script setup>
import { ref } from 'vue'
import Button from './components/Button.vue'
import Score from './components/Score.vue'
import CardWord from './components/CardWord.vue'

const score = ref(100)
const cards = ref([
  {
    word: 'car',
    translation: 'автомобиль',
    state: {
      closed: true,
      opened: false,
    },
    status: {
      success: false,
      fail: false,
      pending: true,
    },
  },
  {
    word: 'dog',
    translation: 'собака',
    state: {
      closed: true,
      opened: false,
    },
    status: {
      success: false,
      fail: false,
      pending: true,
    },
  },
])

const turnCard = (card) => {
  card.state.opened = true
  card.state.closed = false
}

const statusCardSuccess = (card) => {
  card.status.success = true
  card.status.fail = false
}

const statusCardError = (card) => {
  card.status.fail = true
  card.status.success = false
}
</script>

<template>
  <header class="header container">
    <div class="header-title">Запомни слово</div>
    <Score :count="score" />
  </header>
  <main class="main">
    <div class="cards">
      <CardWord
        v-for="card in cards"
        :key="card.word"
        v-bind="card"
        @turn-over="turnCard(card)"
        @status-ok="statusCardSuccess(card)"
        @status-error="statusCardError(card)"
      />
    </div>
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

.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 107px;
}
</style>
