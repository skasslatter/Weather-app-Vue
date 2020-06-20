<template>
  <div id="app">
    <SearchBar @search="updateWeather" />
    <div v-if="forecastData">
      <WeatherForecast v-bind:forecastData="forecastData" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

import SearchBar from "./components/SearchBar";
import WeatherForecast from "./components/WeatherForecast";

export default {
  name: "App",
  data() {
    return {
      forecastData: null
    };
  },
  components: {
    SearchBar,
    WeatherForecast
  },
  methods: {
    updateWeather(data) {
      console.log("testing updateWeather", data);
      const baseUrl = `http://api.weatherbit.io/v2.0/forecast/daily?key=${process.env.VUE_APP_APIKEY}`;
      axios
        .get(`${baseUrl}&city=${data.location},${data.countryCode}&days=10`)
        .then(response => {
          console.log("response from API: ", response.data);
          this.forecastData = response.data.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

body {
  margin: 0px
}

#app {
  height: 100vh;
  width: 100vw;
  font-family: "Poppins", sans-serif;
  background: linear-gradient(
      0deg,
      rgba(255, 255, 255, 0.8),
      rgba(255, 255, 255, 0.8)
    ),
    linear-gradient(
      133.86deg,
      #102f7e -11.47%,
      #0c8dd6 3.95%,
      #1aa0ec 19.37%,
      #60c6ff 34.78%,
      #9bdbff 50.19%,
      #b4deda 65.61%,
      #ffd66b 81.02%,
      #ffc178 96.44%,
      #fe9255 111.85%
    );
}
</style>

