<script setup lang="ts">
import {onMounted, watch, ref} from 'vue'
import {vSelect} from 'components'
const tg = window.Telegram.WebApp;
const onSendData = () => {
  const data = {
    city: selectedCity.value
  }
  tg.sendData(JSON.stringify(data));
  tg.close();
}
onMounted(() => {
  tg.ready();
  tg.MainButton.n
  tg.MainButton.show();
})

watch(
    tg.onEvent("mainButtonClicked", onSendData),
     () => tg.offEvent("mainButtonClicked", onSendData)
)
const selectedCity = ref("")
const cities = ["Almaty", "Astana", "Taraz"]
</script>

<template>
  <div id="container">
    <select name="city" id="city" v-model="selectedCity">
      <option v-for="city in cities">{{ city }}</option>
    </select>

  </div>
</template>

<style scoped>
#container {
  text-align: center;
  margin-top: 10px;
}

button {
  padding: 10px 15px;
  background: var(--tg-theme-button-color);
  color: var(--tg-theme-button-text-color);
  border: none;
  outline: none;
  cursor: pointer;
}
</style>
