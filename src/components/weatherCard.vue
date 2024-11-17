<template>
    <div class="weather-card">
      <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
      <p>{{ weather.weather[0].description }}</p>
      <img
        :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`"
        alt="Weather Icon"
      />

      <p>🌡️ Temp: {{ weather.main.temp }}°C</p>
      <p>💧 Humidity: {{ weather.main.humidity }}%</p>
      <p>💨 Wind Speed: {{ weather.wind.speed }} m/s</p>
    </div>
  </template>
  

<script>
    export default {
    props: ['weather'],
    computed: {
    },
    methods: {
        getIconUrl(icon) {
        return `https://openweathermap.org/img/wn/${icon}@2x.png`;
        },
    },
    };
</script>

  
<style scoped>
  .weather-card {
    color:white;
    background-image: linear-gradient(to bottom right, rgb(47, 71, 255), #000080);
    padding: 20px;
    margin-top: 10px;
    margin-bottom: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

</style>
  