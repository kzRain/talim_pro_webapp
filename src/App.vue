<script setup lang="ts">
import {onMounted, watch} from 'vue'
const tg = window.Telegram.WebApp;
const onSendData = () => {
  tg.sendData("{result:1}");
  tg.close();
}
onMounted(() => {
  tg.ready();
  tg.MainButton.show();
})

watch(
    tg.onEvent("mainButtonClicked", onSendData),
     () => tg.offEvent("mainButtonClicked", onSendData)
)
</script>

<template>
  <div>
    <p>Work</p>
    <button @click="onSendData">Закрыть</button>
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
