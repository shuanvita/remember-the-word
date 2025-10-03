<script setup>
const props = defineProps({
  number: {
    type: Number,
  },
  word: {
    type: String,
  },
  translation: {
    type: String,
  },
  state: {
    type: Object,
  },
  status: {
    type: Object,
  },
})
const emit = defineEmits(['turn-over', 'status-ok', 'status-error'])

const emitTurn = () => {
  emit('turn-over', 'turn')
}

const emitStatusOk = () => {
  emit('status-ok', 'status-ok')
}

const emitStatusError = () => {
  emit('status-error', 'status-error')
}
</script>

<template>
  <div class="card-word">
    <div class="card-word-wrapper">
      <div class="card-word-number">{{ props.number }}</div>
      <div v-if="props.state.closed">
        <div class="card-word-content">{{ props.word }}</div>
        <button class="card-word-turn" @click="emitTurn">Перевернуть</button>
      </div>
      <div v-if="props.state.opened">
        <div class="card-word-content">{{ props.translation }}</div>
        <div class="card-word-actions-buttons">
          <button class="card-word-button-true" @click="emitStatusOk">
            <img src="../assets/true.svg" alt="ok" />
          </button>
          <button class="card-word-button-false" @click="emitStatusError">
            <img src="../assets/false.svg" alt="error" />
          </button>
        </div>
      </div>
      <div v-if="props.status.success">
        <img class="card-word-icon" src="../assets/true.svg" alt="ok" />
      </div>
      <div v-if="props.status.fail">
        <img class="card-word-icon" src="../assets/false.svg" alt="ok" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-word {
  position: relative;
  width: 250px;
  height: 376px;
  padding: 28px 19px;
  background-color: #ffffff;
  border-radius: 16px;
  box-shadow: 0 0 16px 0 rgba(0, 0, 0, 0.1);
}

.card-word-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  border-radius: 12px;
  border: 1px solid #cce8ff;
}

.card-word-number {
  position: absolute;
  top: 22px;
  left: 35px;
  font-size: 14px;
  line-height: 1;
  background-color: #ffffff;
}

.card-word-content {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  font-size: 18px;
}

.card-word-turn {
  position: absolute;
  bottom: 16px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 12px;
  line-height: 1.5;
  letter-spacing: 1.44px;
  font-weight: 700;
  color: var(--color-text-secondary);
  text-transform: uppercase;
  background-color: #ffffff;
}

.card-word-actions-buttons {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  max-width: 97px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  padding: 0 4px;
  background-color: #ffffff;
}

.card-word-icon {
  position: absolute;
  top: 10px;
  left: 50%;
  width: 36px;
  height: 36px;
  transform: translateX(-50%);
}
</style>
