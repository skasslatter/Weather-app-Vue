<template>
  <div>
    <WeatherAverage v-bind:forecastData="forecastData" @average="onAverageUpdate" />
    <WeatherNextWeek v-bind:forecastData="forecastData" />
  </div>
</template>

<script>
import WeatherAverage from "./WeatherAverage";
import WeatherNextWeek from "./WeatherNextWeek";

export default {
  name: "WeatherForecast",
  components: {
    WeatherAverage,
    WeatherNextWeek
  },
  props: {
    forecastData: Array
  },
  methods: {
    onAverageUpdate(average) {
      this.$emit("average", average);
    }
  }
};
</script>
