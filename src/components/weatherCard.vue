<template>
    <div class="weather-card">
      
    <h3 v-if="weather.dt_txt">
      {{ new Date(weather.dt_txt).toDateString() }} <br> 
      {{ cityName }} , {{ country }}
    </h3>
      <h2 v-else>{{ weather.name }}, {{ weather.sys.country }}</h2>
    
      <p>{{ weather.weather[0].description }}</p>
      <img
        :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`"
        alt="Weather Icon"
      />

      <p>🌡️ Temp: {{ weather.main.temp }}°C</p>
      <p>💧 Humidity: {{ weather.main.humidity }}%</p>
      <p>💨 Wind Speed: {{ weather.wind.speed }} m/s</p>

      <!-- ForeCast -->
       <!-- ! add some space and stying! -->
      <div class="forecast">
      <hr v-if="forecast.length">
          <h3 v-if="forecast.length">5-Day Forecast</h3>
          <div class="forecast-list">
              <div v-for="(day, index) in forecast" :key="index" class="forecast-item">
                <p>{{ new Date(day.dt_txt).toDateString() }}</p>
                <p>{{ day.weather[0].description }}</p>
                <img
                  :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`"
                  alt="Weather Icon"
                />
                <p>🌡️ Temp: {{ day.main.temp }}°C</p>
              </div>
            </div>
          </div>
       </div>
</template>
  

<script>
    export default {
    props: {
      weather: { type: Object, required: true },
      forecast: { type: Array, default: () => [] },
      cityName: { type: String, default: '' },
      country: { type: String, default: '' }
    },
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
  color: white;
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
  margin-top: 20px;
  margin-bottom: 20px;
  width: auto;
  background-image: linear-gradient(to bottom right, rgb(47, 71, 255), #000080);
}

.weather-card img {
  width: 100px;
  height: 100px;
}


  .forecast{
    padding-top: 10px;
    h3{
      font-weight: 500;
    }
  }

  .forecast-list{
    display: flex;
    gap:10px;
  }

</style>
  