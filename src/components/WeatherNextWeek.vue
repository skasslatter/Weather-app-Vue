<template>
  <div class="weeklyForecast">
    <div v-for="(day, index) in nextWeekTemperatures" :key="index">
      <div>{{day.dayOfTheWeek}}</div>
      <div>{{day.temp}}</div>
    </div>
  </div>
</template>

<script>
import { DateTime } from "luxon";

export default {
  name: "WeatherForecast",
  data() {
    return {};
  },
  components: {},
  methods: {},
  props: {
    forecastData: Array
  },
  computed: {
    nextWeekTemperatures: function() {
      if (!this.forecastData) {
        return null;
      }
      let arr = [];
      for (let i = 0; i < 7; i++) {
        let date = DateTime.fromISO(this.forecastData[i].datetime);
        let dayOfTheWeek = date
          .setLocale("en-US")
          .toLocaleString({ weekday: "long" });
        let temp = this.forecastData[i].temp;
        arr.push({ dayOfTheWeek, temp });
      }
      return arr;
    }
  }
};
</script>

<style scoped>
.weeklyForecast {
  flex-direction: row;
  display: flex;
  justify-content: space-around;
}
</style>