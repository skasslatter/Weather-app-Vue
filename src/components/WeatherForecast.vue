<template>
  <div>
    <WeatherToday/>
  </div>
</template>

<script>
import WeatherToday from "./WeatherToday";


export default {
  name: "WeatherForecast",
  data() {
    return {};
  },
  components: {
    WeatherToday,
  },
  methods: {}
};
</script>

<style scoped>
</style>
