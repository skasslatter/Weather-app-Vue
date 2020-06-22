<template>
  <div id="app" v-bind:style="{ background: backgroundColor}">
    <SearchBar @search="updateWeather" />
    <div v-if="loading">Loading...</div>
    <div v-else-if="errorMessage">{{errorMessage}}</div>
    <div v-else-if="forecastData">
      <WeatherForecast v-bind:forecastData="forecastData" @average="setBackground" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

import SearchBar from "./components/SearchBar";
import WeatherForecast from "./components/WeatherForecast";
const initialBackground =
  "linear-gradient(0deg, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.8)), linear-gradient(133.86deg, #102f7e -11.47%, #0c8dd6 3.95%, #1aa0ec 19.37%, #60c6ff 34.78%, #9bdbff 50.19%, #b4deda 65.61%, #ffd66b 81.02%, #ffc178 96.44%, #fe9255 111.85%)";

export default {
  name: "App",
  data() {
    return {
      forecastData: null,
      loading: false,
      errorMessage: null,
      backgroundColor: initialBackground
    };
  },
  components: {
    SearchBar,
    WeatherForecast
  },
  methods: {
    updateWeather(data) {
      this.loading = true;
      console.log("testing updateWeather", data);
      const baseUrl = `http://api.weatherbit.io/v2.0/forecast/daily?key=${process.env.VUE_APP_APIKEY}`;
      axios
        .get(`${baseUrl}&city=${data.location},${data.countryCode}&days=10`)
        .then(response => {
          this.loading = false;
          console.log("response from API: ", response.data);
          if (!response.data) {
            this.errorMessage = "Please enter a valid city";
          } else {
            this.forecastData = response.data.data;
            this.errorMessage = null;
          }
        })
        .catch(error => {
          console.log(error);
          this.errorMessage = "Failed to fetch forecast data";
        });
    },
    setBackground(average) {
      const gradientPercentages = [0, 12.5, 25, 37.5, 50, 62.5, 75, 87.5, 100];
      const increaseFactor = 3

      let percentageOfAverageTemp = average / 0.8;
      let gradientModifier = percentageOfAverageTemp * increaseFactor;
      let newGradientPercentages = gradientPercentages.map(value => {
        return (value - 50) * increaseFactor - gradientModifier + 100;
      });
      console.log(newGradientPercentages);
      let newBackgroundGradient = `linear-gradient(145.74deg, #102F7E ${newGradientPercentages[0]}%, #0C8DD6 ${newGradientPercentages[1]}%, #1AA0EC ${newGradientPercentages[2]}%, #60C6FF ${newGradientPercentages[3]}%, #9BDBFF ${newGradientPercentages[4]}%, #B4DEDA ${newGradientPercentages[5]}%, #FFD66B ${newGradientPercentages[6]}%, #FFC178 ${newGradientPercentages[7]}%, #FE9255 ${newGradientPercentages[8]}%);`;
      console.log(newBackgroundGradient);
      this.backgroundColor = newBackgroundGradient;
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

body {
  margin: 0px;
}

#app {
  height: 100vh;
  width: 100vw;
  font-family: "Poppins", sans-serif;
  /* background: linear-gradient(
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
    ); */
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
</style>

