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
  props: {
    forecastData: Array
  },
  computed: {
    nextWeekTemperatures: function() {
      if (!this.forecastData) {
        return null;
      }
      const arr = [];
      for (let i = 0; i < 7; i++) {
        const date = DateTime.fromISO(this.forecastData[i].datetime);
        const dayOfTheWeek = date
          .setLocale("en-US")
          .toLocaleString({ weekday: "long" });
        const temp = Math.round(this.forecastData[i].temp);
        arr.push({ dayOfTheWeek, temp });
      }
      return arr;
    }
  }
};
</script>

<style scoped>
.week-container {
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
  font-size: 12px;
  line-height: 24px;
  letter-spacing: 0.06em;
  color: #08153e;
}

.temp-container {
  display: flex;
}

.temp {
  font-size: 24px;
  line-height: 32px;
  color: #ffffff;
}

.celsius {
  font-size: 14px;
  line-height: 24px;
  color: #ffffff;
}
</style>