<template>
  <div id="app">
    <SearchBar @search="updateWeather" />
    <WeatherForecast v-bind:forecastData="forecastData" />
  </div>
</template>

<script>
import axios from "axios";
import { DateTime } from "luxon";
DateTime.local();

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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

