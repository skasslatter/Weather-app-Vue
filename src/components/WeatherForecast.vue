<template>
  <div>
    <WeatherAverage v-bind:forecastData="forecastData"/>
  </div>
</template>

<script>
import WeatherAverage from "./WeatherAverage";


export default {
  name: "WeatherForecast",
  data() {
    return {

    };
  },
  components: {
    WeatherAverage,
  },
  methods: {},
  props: {
    forecastData: Array,
  },
};
</script>

<style scoped>
</style>
