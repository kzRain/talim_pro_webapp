<script setup lang="ts">
import { onMounted } from 'vue'
const tg = window.Telegram.WebApp;
onMounted(() => {
  tg.ready();
  tg.MainButton.show();
})
</script>

<template>
  <div>
    <p>Work</p>
    <button @click="tg.close()">Закрыть</button>
  </div>
</template>

<style scoped>
button {
  padding: 10px 15px;
  background: var(--tg-theme-button-color);
  color: var(--tg-theme-button-text-color);
  border: none;
  outline: none;
  cursor: pointer;
}
</style>
