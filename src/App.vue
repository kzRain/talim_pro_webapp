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
    <h2>Город</h2>
    <select name="city" id="city" v-model="selectedCity">
      <option v-for="city in cities">{{ city }}</option>
    </select>
    <h2>Школа</h2>
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

select {
  display: block;
  font-size: 16px;
  font-family: sans-serif;
  font-weight: 700;
  color: #444;
  line-height: 1.3;
  padding: .6em 1.4em .5em .8em; width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  margin: 0;
  border: 1px solid #aaa;
  box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
  border-radius: .5em;
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  background-color: #fff;
  background-repeat: no-repeat, repeat;
  background-position: right .7em top 50%, 0 0;
  background-size: .65em auto, 100%;
}
select-css::-ms-expand { display: none; }
select-css:hover { border-color: #888; }
select-css:focus { border-color: #aaa;
  box-shadow: 0 0 1px 3px rgba(59, 153, 252, .7);
  box-shadow: 0 0 0 3px -moz-mac-focusring;
  color: #222;
  outline: none;
}
select option { font-weight:normal; }
*[dir="rtl"] .select-css, :root:lang(ar) .select-css, :root:lang(iw) .select-css {
  background-position: left .7em top 50%, 0 0;
  padding: .6em .8em .5em 1.4em;
}

</style>
