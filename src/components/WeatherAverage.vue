<template>
  <div>
    <div>{{dateString}}</div>
    <div>{{this.averageTemperature}} °C</div>
  </div>
</template>

<script>
//to get the date
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
    averageTemperature: function() {
      if (!this.forecastData) {
        return null;
      }
      let arr = [];
      for (let i = 0; i < this.forecastData.length; i++) {
        arr.push(this.forecastData[i].temp);
      }
      let sum = 0;
      for (let i = 0; i < arr.length; i++) {
        sum = sum + arr[i];
      }
      let average = (sum / arr.length).toFixed(1);
      return average;
    },
    dateString: function() {
      const startDate = DateTime.fromISO(this.forecastData[0].datetime);
      const endDate = DateTime.fromISO(
        this.forecastData[this.forecastData.length - 1].datetime
      );
      const startMonth = startDate
        .setLocale("en-US")
        .toLocaleString({ month: "long" });
      const endMonth = endDate
        .setLocale("en-US")
        .toLocaleString({ month: "long" });

      if (startDate.year !== endDate.year) {
        return `${startMonth} ${startDate.day} ${startDate.year} - ${endMonth.month} ${endDate.day} ${endDate.year}`;
      } else if (startDate.month !== endDate.month) {
        return `${startMonth} ${startDate.day} - ${endMonth.month} ${endDate.day} ${startDate.year}`;
      } else {
        return `${startMonth} ${startDate.day} - ${endDate.day} ${startDate.year}`;
      }
    }
  }
};
</script>

<style scoped>
</style>
