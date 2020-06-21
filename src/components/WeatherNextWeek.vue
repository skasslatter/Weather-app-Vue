<template>
  <div class="week-container">
    <div class="day-container" v-for="(day, index) in nextWeekTemperatures" :key="index">
      <div class="weekday">{{day.dayOfTheWeek}}</div>
      <div class="temp-container">
        <div class="temp">{{day.temp}}</div>
        <div class="celsius">°C</div>
      </div>
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
        let temp = Math.round(this.forecastData[i].temp);
        arr.push({ dayOfTheWeek, temp });
      }
      return arr;
    }
  }
};
</script>

<style scoped>
.week-container {
  flex-direction: row;
  display: flex;
  justify-content: space-around;
  width: 632px;
}

.day-container {
  display: flex;
  flex-direction: column;
  place-items: center;
}

.weekday {
  text-transform: uppercase;
  font-family: Poppins;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 24px;

  display: flex;
  align-items: center;
  text-align: center;
  letter-spacing: 0.06em;

  color: #08153e;
}

.temp-container {
  display: flex;
}

.temp {
  font-family: Poppins;
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 32px;

  color: #ffffff;
}

.celsius {
  font-family: Poppins;
  font-style: normal;
  font-weight: 600;
  font-size: 14px;
  line-height: 24px;

  color: #ffffff;
}
</style>