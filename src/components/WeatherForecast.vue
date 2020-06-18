<template>
  <div>
    <WeatherAverage />
  </div>
</template>

<script>
import WeatherAverage from "./WeatherAverage";


export default {
  name: "WeatherForecast",
  data() {
    return {};
  },
  components: {
    WeatherAverage,
  },
  methods: {},
  props: {
    weatherForecast: Array,
  },
};
</script>

<style scoped>
</style>
