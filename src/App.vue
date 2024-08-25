<template>
  <div class="App">
    <Weather/>
  </div>
</template>

<script setup>
import Weather from './components/Weather.vue';


</script>

<style lang="scss" scoped>
body{
  margin: 0;
  padding: 0;
}

.App{
  text-align: center;
  width: 90%;
  margin: 50px auto 0;
  height: 470px;
  padding: 20px 15px;
  max-width: 700px;
  border-radius: 20px;
  background: #03ff9a;
  box-shadow: 10px 10px #000;
}
</style>