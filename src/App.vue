<template>
  <div id="app" class="container content">
    <h1 style="margin-top: 10px;">Weather App</h1>
    <input type="text" v-model="city" @keyup.enter="getWeather" placeholder="Enter city name"/>
    <button @click="getWeather">Get Weather</button>

     
    <div v-if="weather">
      <WeatherCard :weather="weather"
      :forecast = "forecast"/>
    </div>
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
      forecast : [],
      apiKey: '__API_KEY__', 
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

        const forecastRes = await axios.get(
          `https://api.openweathermap.org/data/2.5/forecast?q=${this.city}&appid=${this.apiKey}&units=metric`
        );

        this.forecast = forecastRes.data.list.filter(item =>
          item.dt_txt.includes("12:00:00")
        );
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
  font-size: large;
  padding: 10px;
  /* margin-right: 10px; */
  border: 1px solid #ddd;
  border-radius: 5px;
  width: auto;
}

button {
  font-size: large;
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

</style>
