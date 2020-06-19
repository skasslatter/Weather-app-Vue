<template>
  <div>
    <div>{{today}} - {{todayPlus10}} {{currentYear}}</div>
    <div>{{this.averageTemperature}} °C</div>
  </div>
</template>

<script>
import { DateTime } from "luxon";
DateTime.local();

var timeAndDate = DateTime.local();
var monthDay = {month: 'long', day: 'numeric'};
var year = {year: 'numeric'}
var today = timeAndDate.setLocale('en-US').toLocaleString(monthDay) 
var todayPlus10 = timeAndDate.plus({days: 7}).setLocale('en-US').toLocaleString(monthDay) 
var currentYear = timeAndDate.setLocale('en-US').toLocaleString(year) 

export default {
  name: "WeatherForecast",
  data() {
    return {
      today,
      todayPlus10,
      currentYear
    };
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
      console.log("arr", arr);
      let sum = 0;
      for (let i = 0; i < arr.length; i++) {
        sum = sum + arr[i];
      }
      console.log("sum", sum);
      let average = (sum / arr.length).toFixed(1);
      return average;
    }
  }
};
</script>

<style scoped>
</style>
