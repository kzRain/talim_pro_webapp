<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
const tg = window.Telegram.WebApp;
</script>

<template>
  <div>
    <p>Work</p>
    <button @click="tg.close()">Закрыть</button>
  </div>
</template>

<style scoped>

</style>
