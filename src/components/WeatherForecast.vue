<template>
  <div>
    <WeatherAverage v-bind:forecastData="forecastData" />
    <WeatherNextWeek v-bind:forecastData="forecastData" />
  </div>
</template>

<script>
import WeatherAverage from "./WeatherAverage";
import WeatherNextWeek from "./WeatherNextWeek";

export default {
  name: "WeatherForecast",
  data() {
    return {
      
    };
  },
  components: {
    WeatherAverage,
    WeatherNextWeek
  },
  methods: {},
  props: {
    forecastData: Array
  }
};
</script>

<style scoped>
</style>
