<script setup lang="ts">
import {onMounted, watch, ref} from 'vue'

const tg = window.Telegram.WebApp;
const onSendData = () => {
  const data = {
    webAppQueryId: queryId,
    city: selectedCity.value
  }
  if (queryId !== "") {
    const requestOptions = {
      method: "POST",
      headers: {"Content-Type": "application/json",
        "Access-Control-Allow-Origin": "*"
      },
      body: JSON.stringify(data)
    };
    tg.MainButton.text = JSON.stringify(data);
    fetch('http://devtg.courstore.com/web-app', requestOptions)
    //     .then((response) => {
    //           console.log(response);
    //           tg.close();
    //         }
    //     ).catch((error) => {
    //       tg.MainButton.text = error
    //     }
    // );
    // tg.MainButton.text = "Request sended"
  } else {
    tg.sendData(JSON.stringify(data));
    tg.close();
  }
}
let queryId = "";

onMounted(() => {
  tg.ready();
  queryId = tg.initDataUnsafe?.query_id;
})

watch(
    tg.onEvent("mainButtonClicked", onSendData),
    () => tg.offEvent("mainButtonClicked", onSendData)
)
const selectedRegion = ref("")
const selectedCity = ref("")
const regions = [{
  name: "Алматинская область",
  cities: ["Талгар", "Каскелен", "Кеген", "Узынагаш"]
}, {
  name: "Талдыкорганская область",
  cities: ["Учарал", "Конаев", "Сары-Қзек"]
}]
let cities = ref([""])
const onChange = (event) => {
  let selectedCities = regions.find(region => region.name === event.target.value);
  if (selectedCities?.cities !== undefined) {
    cities.value = selectedCities.cities;
  }
}

watch(selectedCity, (value) => {
  console.log(value);
  if (value === "") {
    tg.MainButton.hide();
  } else {
    tg.MainButton.show();
    tg.MainButton.text = `Выбрать город ${value}`;
  }
})
</script>

<template>
  <div id="container">
    <h2>Регион</h2>
    <select name="city" id="city" v-model="selectedRegion" @change="onChange($event)">
      <option v-for="region in regions">{{ region.name }}</option>
    </select>
    <h2>Населенный пункт</h2>
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
  padding: .6em 1.4em .5em .8em;
  width: 100%;
  max-width: 100%;
  box-sizing: border-box;
  margin: 0;
  border: 1px solid #aaa;
  box-shadow: 0 1px 0 1px rgba(0, 0, 0, .04);
  border-radius: .5em;
  -moz-appearance: none;
  -webkit-appearance: none;
  appearance: none;
  background-color: #fff;
  background-repeat: no-repeat, repeat;
  background-position: right .7em top 50%, 0 0;
  background-size: .65em auto, 100%;
}

select-css::-ms-expand {
  display: none;
}

select-css:hover {
  border-color: #888;
}

select-css:focus {
  border-color: #aaa;
  box-shadow: 0 0 1px 3px rgba(59, 153, 252, .7);
  box-shadow: 0 0 0 3px -moz-mac-focusring;
  color: #222;
  outline: none;
}

select option {
  font-weight: normal;
}

*[dir="rtl"] .select-css, :root:lang(ar) .select-css, :root:lang(iw) .select-css {
  background-position: left .7em top 50%, 0 0;
  padding: .6em .8em .5em 1.4em;
}

</style>
