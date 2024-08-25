<template>
  <div>
    <Search :search="search" @updateSearch="updateSearch" />
    <div>
      <div class="city-name">
        <h2>
          {{ weatherData?.name }},<span>{{ weatherData?.sys?.country }}</span>
        </h2>
      </div>
      <div class="date">
        <h2>{{ getCurrentDate() }}</h2>
      </div>
      <div class="temp">{{ weatherData?.main?.temp }}&deg;C</div>
      <p class="description">
        {{
          weatherData && weatherData.weather && weatherData.weather[0]
            ? weatherData.weather[0].description
            : ""
        }}
      </p>
      <div class="weather-info">
        <div class="column">
          <div>
            <p class="wind">{{ weatherData?.wind?.speed }}</p>
            <p>Wind Speed</p>
          </div>
        </div>
        <div class="column">
          <div>
            <p class="humidity">{{ weatherData?.main?.humidity }}</p>
            <p>Humidity</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Search from "./search.vue";

const weatherData = ref(null);
const search = ref("");
const loading = ref(false);

async function fetchWeatherData(param) {
  loading.value = true;
  try {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${param}&lang=zh_cn&appid=5a0d729d26b96051152aae0dfe6a268e&units=metric`
    );
    const data = await response.json();
    console.log(data);

    if (data) {
      weatherData.value = data;
      loading.value = false;
    }
  } catch (error) {
    console.log(error);
    loading.value = false;
  } finally {
    loading.value = false;
  }
}

const getCurrentDate = () => {
  return new Date().toLocaleDateString("en-us", {
    month: "long",
    weekday: "long",
    year: "numeric",
    day: "numeric",
  });
};

const updateSearch = (newSearch) => {
  search.value = newSearch;
  fetchWeatherData(search.value);
};

onMounted(() => {
  fetchWeatherData("dongguan");
});
</script>

<style lang="scss" scoped>

.city-name {
  margin-bottom: 10px;
}

.loading {
  font-size: 60px;
  font-weight: bolder;
  color: #000;
}

.date {
  font-size: 18px;
  font-weight: 500;
  font-style: italic;
}

.temp {
  font-size: 64px;
  color: #000;
  font-weight: bold;
  text-align: center;
}

.description {
  color: #000;
  font-size: 22px;
  font-weight: 500;
  margin-top: 0;
  margin-bottom: 20px;
}

.weather-info {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 20px;
  padding: 0 20px;
  font-size: 20px;
  font-weight: bold;
  text-align: center;
}

.column {
  display: flex;
  align-items: center;
  line-height: 5px;
}
</style>
