<script setup>
const props = defineProps({
  count: {
    type: Number,
  },
});
</script>

<template>
  <div class="score">
    <div class="score-total">{{ props.count }}</div>
    <img src="../assets/heart.svg" alt="hearth" />
  </div>
</template>

<style scoped>
.score {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 24px;
  border-radius: 36px;
  background-color: #cce8ff;
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.15);
}

.score-total {
  color: var(--color-bg-button);
  font-weight: 700;
}
</style>
