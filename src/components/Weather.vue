<template>
  <div class="centered-content">
    <div class="widget-header">
      <h2 class="widget-title">CARI INFORMASI CUACA DI KOTA MU!</h2>
    </div>
    <q-input
      filled
      v-model="searchQuery"
      label="Masukkan Nama Kota"
      class="location-input"
    />
    <q-btn @click="searchWeather" class="search-button">Cari</q-btn>
    <div v-if="loading" class="loading-message">Loading data...</div>
    <div v-else-if="weatherData" class="weather-result">
      <div class="weather-info">
        <p class="city-name">{{ weatherData.name }}</p>
        <p class="temperature">{{ weatherData.main.temp }}°C</p>
        <img
          :src="getWeatherIconUrl(weatherData.weather[0].icon)"
          :alt="weatherData.weather[0].description"
          class="weather-icon"
        />
        <p class="weather-description">{{ weatherData.weather[0].description }}</p>
      </div>
      <div class="additional-info">
        <p>Kelembaban: {{ weatherData.main.humidity }}%</p>
        <p>Kecepatan Angin: {{ weatherData.wind.speed }} m/s</p>
      </div>
    </div>
    <div v-else-if="error" class="error-message">{{ error }}</div>
  </div>
</template>

<script>
import { ref } from "vue";
import axios from "axios";
import { QInput, QBtn } from "quasar";

export default {
  components: { QInput, QBtn },
  setup() {
    const searchQuery = ref("");
    const weatherData = ref(null);
    const loading = ref(false);
    const error = ref(null);

    const searchWeather = async () => {
      loading.value = true;
      error.value = null;

      try {
        const response = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${searchQuery.value}&appid=bcbc6cc1860d02bd1f4306314c08d7e0&units=metric`
        );
        if (response.data.cod !== 200) {
          throw new Error("City not found");
        }
        weatherData.value = response.data;
      } catch (error) {
        console.error(error);
        error.value =
          "Gagal mengambil data cuaca atau kota tidak ditemukan";
      } finally {
        loading.value = false;
      }
    };

    const getWeatherIconUrl = (iconCode) => {
      return `https://openweathermap.org/img/wn/${iconCode}.png`;
    };

    return {
      searchQuery,
      weatherData,
      loading,
      error,
      searchWeather,
      getWeatherIconUrl,
    };
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap');

.centered-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-image: url('https://images.pexels.com/photos/1118873/pexels-photo-1118873.jpeg');
  background-size: cover;
  background-position: center;
  padding: 20px;
  box-sizing: border-box;
  text-align: center;
  color: #ffffff;
}

.widget-header {
  margin-bottom: 20px;
}

.widget-title {
  font-size: 2rem;
  color: #333333;
  font-family: 'Montserrat', sans-serif;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.location-input {
  width: 100%;
  max-width: 400px;
  margin-bottom: 15px;
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 10px;
}

.search-button {
  width: 100%;
  max-width: 400px;
  padding: 12px 0;
  background-color: #333333;
  color: #ffffff;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.search-button:hover {
  background-color: #555555;
  transform: translateY(-3px);
}

.loading-message {
  font-style: italic;
  color: #333333;
  margin-top: 15px;
}

.weather-result {
  margin-top: 25px;
}

.weather-info {
  margin-bottom: 15px;
}

.city-name {
  font-weight: 600;
  color: #ffffff;
  font-size: 1.8rem;
  font-family: 'Montserrat', sans-serif;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.temperature {
  font-size: 3.5rem;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.weather-icon {
  width: 80px;
  height: 80px;
  margin: 0 auto;
}

.weather-description {
  font-style: italic;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.additional-info {
  margin-top: 15px;
}

.additional-info p {
  margin: 5px 0;
  color: #ffffff;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.error-message {
  color: #ff0000;
  margin-top: 15px;
  text-align: center;
}
</style>
