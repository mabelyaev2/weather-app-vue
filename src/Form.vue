<template>
      <div class="weather-info">
        <img src="@/assets/mountain.jpg" alt="mountain-pic">
        <div class="weather-info_introduction">
          <h1 class="weather-info__head">Weather app</h1>
          <form @submit.prevent="WeatherInfo" class="weather-info__inputs">
            <input type="text" @keyup.enter="WeatherInfo" v-model="city" placeholder="insert the city">
            <button class="btn" type="submit">Check</button>
          </form>
          <ul>
            <li>Country: {{ country }}</li>
            <li>Current temperature (Celsium/Fahrenheit): {{ temp }}°C | {{fahrTemp}}°F </li>
            <li>Wind speed: {{ wind }} m/s</li>
            <li>Pressure: {{ pressure }}</li>
            <li>Sunset: {{ sunsetTime }}</li>
          </ul>
        </div>
      </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
      return {
        city: '',
        country:'',
        temp:'',
        fahrTemp:'',
        wind:'',
        pressure:'',
        sunset:'',
        sunriseTime: '',
        sunsetTime: '',
      }
    },
    methods: {
      WeatherInfo() {
        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=a89e0631bdb1b1f37f60febba944d226&units=metric`)
        .then(response => {
          this.city = response.data.name;
          this.country = response.data.sys.country;
          this.temp = parseInt(response.data.main.temp);
          this.wind = response.data.wind.speed;
          this.pressure = response.data.main.pressure;
          this.sunset = response.data.sys.sunset;

          const sunset = this.sunset;
          const date1 = new Date();
          date1.setTime(sunset);
          this.sunsetTime = date1.getHours() + ":" + date1.getMinutes();
          this.fahrTemp = parseInt((this.temp * 1.8) + 32);
        });
      }
    },
  }
</script>

<style>
    .weather-info {
      margin: 0 auto;
      margin-top: 100px;
      width: 800px;
      height: 400px;
      background-image: linear-gradient(to right top, #166ced, #5c7ee9, #8090e4, #9ca3df, #b5b7da);
      border-radius: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: Helvetica, sans-serif;
    }

    img {
      height: 400px;
      margin-right: auto;
    }

    .weather-info__head {
      margin-right: auto;
      font-weight: bold;
      font-size: 30px;
    }

    .weather-info_introduction {
      display: flex;
      align-items: flex-end;
      flex-direction: column;
      margin: 0 auto;
      margin-left: 0;
    }

    ul {
        margin-right: auto;
    }

    li {
        padding-bottom: 10px;
    }

    input {
        min-width: 300px;
        min-height: 25px;
        border-radius: 3px;
        padding-left: 8px;
    }

    .btn {
        margin-left: 10px;
        min-height: 31px;
        border-radius: 3px;
        box-shadow: none;
    }
</style>