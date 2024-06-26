<template>
  <div id="app">
    <br>
    <q-card class="weather-widget">
      <q-card-section>
        <h1 class="judul">Uas Prak</h1>
        <q-form @submit.prevent="updateWeather">
          <q-input
            v-model="city"
            placeholder="Enter city"
            outlined
            dense
            class="q-mb-md"
          />
          <q-btn type="submit" label="Search" color="positive" class="search-btn" />
        </q-form>
      </q-card-section>
      <q-card-section class="barudak" v-if="weather">
        <div class="weather-info">
          <p>Location: <span class="highlight">{{ weather.name }}</span></p>
          <p>Temperature: <span class="highlight">{{ weather.main.temp }} °C</span></p>
          <p>Weather: <span class="highlight">{{ weather.weather[0].description }}</span></p>
          <img :src="getIconUrl(weather.weather[0].icon)" alt="Weather icon" class="weather-icon" />
        </div>
      </q-card-section>
      <q-card-section v-else>
        <p>Loading...</p>
      </q-card-section>
    </q-card>
  </div>
</template>

<script>
export default {
  name: 'WeatherWidget',
  data() {
    return {
      weather: null,
      city: '',
      API_KEY: '920dbb38dd7b1767bdf6d26ceacb11e7',
      BASE_URL: 'https://api.openweathermap.org/data/2.5/weather',
      UNITS: 'metric'
    };
  },
  methods: {
    async fetchWeather() {
      if (!this.city) return;
      try {
        const response = await fetch(`${this.BASE_URL}?q=${this.city}&units=${this.UNITS}&appid=${this.API_KEY}`);
        const data = await response.json();
        this.weather = data;
        this.updateBackground(this.weather.main.temp);
      } catch (error) {
        console.error('Error fetching weather data:', error);
      }
    },
    updateWeather() {
      this.fetchWeather();
    },
    updateBackground(temp) {
      const body = document.body;
      body.classList.remove('cold-weather', 'cool-weather', 'warm-weather', 'hot-weather');

      if (temp <= 0) {
        body.classList.add('cold-weather');
      } else if (temp > 0 && temp <= 20) {
        body.classList.add('cool-weather');
      } else if (temp > 20 && temp <= 30) {
        body.classList.add('warm-weather');
      } else {
        body.classList.add('hot-weather');
      }
    },
    getIconUrl(iconCode) {
      return `https://openweathermap.org/img/wn/${iconCode}@2x.png`;
    }
  },
  mounted() {
    this.fetchWeather();
  }
};
</script>

<style scoped>
body {
  background-color: #f0f0f0;
}

.barudak {
  justify-content: center;
  align-items: center;
  text-align: center;
  font-weight: bolder;
  color: #010d1a;
}

.background-blur {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px); /* For Safari */
  z-index: -1; /* Ensure it is behind other elements */
}

.q-mb-md {
  background-color: rgba(255, 255, 255, 0.85);
}

.weather-widget {
  position: relative;
  font-family: Arial, sans-serif;
  border: 1px solid #ccc;
  border-radius: 20px;
  color: white;
  width: 100%;
  max-width: 400px;
  margin: 4rem auto;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px); 
  opacity: 0.85; 
  margin-bottom: 2px;
}

.weather-widget * {
  position: relative;
  z-index: 1; 
}

.judul {
  color: #ffce00;
  font-weight: 750;
  font-size: 1.5em;
}

h1 {
  font-size: 28px;
  text-align: center;
  margin-bottom: 20px;
}

form {
  margin-bottom: 16px;
  text-align: center;
}

input {
  padding: 8px;
  margin-right: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.search-btn {
  width: 100%;
  margin-top: 10px;
}

.highlight {
  font-weight: bold;
  color: #ffce00;
}

.weather-info {
  text-align: center;
}

.weather-icon {
  width: 100px;
  height: 100px;
}
</style>
