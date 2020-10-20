<template>
  <div>
    <div class="container">
      <h1>Weather App</h1>
      <div>
        <h2>Todays Weather Data</h2>
        <div>
          <p>Location: {{ location }}</p>
          <ul v-if="apiData">
            <li>Temp: {{ (apiData.temp - 273.15).toFixed(2) }}&#8451;</li>
            <li>
              Max Temp: {{ (apiData.temp_max - 273.15).toFixed(2) }}&#8451;
            </li>
            <li>
              Min Temp: {{ (apiData.temp_min - 273.15).toFixed(2) }}&#8451;
            </li>
            <li>
              Feels Like: {{ (apiData.feels_like - 273.15).toFixed(2) }}&#8451;
            </li>
            <li>Humidity: {{ apiData.humidity }}%</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      apiData: null,
      location: ''
    }
  },
  created() {
    axios
      .get(
        'http://api.openweathermap.org/data/2.5/weather?q=Dhaka,BD&APPID=41177bba6c535be0bb4500b47ff24769'
      )
      .then(res => {
        const location = res.data.name
        const data = res.data.main

        this.location = location
        this.apiData = data

        console.log(res.data)
      })
  }
}
</script>

<style scopped>
body {
  font-family: Arial, Helvetica, sans-serif;
}
.container {
  max-width: 50%;
  border: 2px solid gray;
  border-radius: 10px;
  margin: 0 auto;
  padding: 20px;
}
</style>
