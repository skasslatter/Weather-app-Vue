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
  data() {
    return {};
  },
  components: {
    WeatherAverage,
    WeatherNextWeek
  },
  methods: {
    onAverageUpdate(newValue) {
      this.average = newValue;
      this.$emit("average", this.average);
    }
  },
  props: {
    forecastData: Array
  }
};
</script>

<style scoped>
</style>
