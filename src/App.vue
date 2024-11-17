<template>
  <div id="app" class="container content">
    <h1 style="margin-top: 10px;">Weather App</h1>
    <input type="text" v-model="city" @keyup.enter="getWeather" placeholder="Enter city name"/>
    <button @click="getWeather">Get Weather</button>

    <WeatherCard v-if="weather" :weather="weather"/>
  </div>
</template>

<script>
import axios from 'axios';
import WeatherCard from './components/weatherCard.vue';

export default {
  data() {
    return {
      city: 'Bangkok', // set default to bangkok
      weather: null,
      apiKey: '__MY_API_KEY__', 
    };
  },
  methods: {
    async getWeather() {
      if (this.city.trim() === '') return;

      try {
        const response = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${this.apiKey}&units=metric`
        );
        this.weather = response.data;
      } catch (error) {
        console.error('Error fetching weather:', error);
        alert('City not found!');
      }
    },
  },
  async mounted() {
    await this.getWeather(); //fetch weather data for default city on app load
  },
  components: {
    WeatherCard,
  },
};
</script>

<style>


#app {
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  /* justify-content: center; */
  /* min-height: 100vh; */
  /* background-color: #f7f7f7; */
  /* padding: 20px; */
}

.content{
  box-shadow: 5px 10px 18px #888888;
  color:black;
  background-color: #f7f7f7;
  /* border: 1px solid; */
  padding : 20px;
  border-radius: 10px;
}

input {
  padding: 10px;
  /* margin-right: 10px; */
  border: 1px solid #ddd;
  border-radius: 5px;
  width: 300px;
}

button {
  margin-top: 10px;
  margin-bottom: 10px;
  padding: 10px;
  border: none;
  background-color: #3498db;
  color: white;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2980b9;
}

.weather-card {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  margin-top: 20px;
  width: 300px;
}

.weather-card img {
  width: 100px;
  height: 100px;
}
</style>
