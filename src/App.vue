<template>
  <div id="app">
    <SearchBar @search="updateWeather"/>
    <WeatherForecast />
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";
import WeatherForecast from "./components/WeatherForecast";

export default {
  name: "App",
  components: {
    SearchBar,
    WeatherForecast,
  },
  methods: {
    updateWeather(data) {
      console.log("testing updateWeather", data);
      axios
        .get(`http://api.weatherbit.io/v2.0/current?key=${process.env.VUE_APP_APIKEY}&city=${data.location}&country=${data.countryCode}`)
        .then(response => {
          console.log("response: ", response);
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

