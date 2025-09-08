<script setup></script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  min-width: 335px;
  padding: 16px 10px;
  border-radius: 100px;
  border: none;
  background: none;
  font-family: inherit;
  font-size: 24px;
  line-height: 1.5;
  color: #ffffff;
  background-color: var(--color-bg-button);
  cursor: pointer;
}

.button:hover {
  background-color: var(--color-bg-button-hover);
}
</style>
