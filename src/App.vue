<script setup>
import { onMounted, ref } from 'vue'
import Button from './components/Button.vue'
import Score from './components/Score.vue'
import CardWord from './components/CardWord.vue'

const API_ENDPOINT = 'http://localhost:8080/api/random-words'

const score = ref(100)
const isStartGame = ref(false)
const cards = ref([])

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

const getWords = async () => {
  try {
    isStartGame.value = true
    const res = await fetch(API_ENDPOINT)
    if (res.status !== 200) {
      cards.value = null
    }
    const data = await res.json()
    cards.value = data.map((word) => ({
      ...word,
      state: {
        closed: true,
        opened: false,
      },
      status: {
        success: false,
        fail: false,
        pending: true,
      },
    }))
  } catch (error) {
    console.error('Ошибка:', error)
  }
}
</script>

<template>
  <header class="header container">
    <div class="header-title">Запомни слово</div>
    <Score :count="score" />
  </header>
  <main class="main">
    <div v-if="isStartGame" class="cards">
      <CardWord
        v-for="(card, idx) in cards"
        :key="card.word"
        v-bind="card"
        :number="idx + 1"
        @turn-over="turnCard(card)"
        @status-ok="statusCardSuccess(card)"
        @status-error="statusCardError(card)"
      />
    </div>
    <Button v-if="!isStartGame" class="start-game-button" @click="getWords">Начать игру</Button>
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

.start-game-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
</style>
