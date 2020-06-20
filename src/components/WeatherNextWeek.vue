<template>
  <div class="weeklyForecast">
    <div v-for="(day, index) in nextWeekTemperatures" :key="index">
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
.weeklyForecast {
  flex-direction: row;
  display: flex;
  justify-content: space-around;
}

.weekday {
  text-transform: uppercase;
}

.temp-container {
  display: flex;
}

.temp {
  font-weight: 600;
  font-size: 24px;
  line-height: 32px;
  /* color: #FFFFFF; */
}

.celsius {
  font-weight: 600;
  font-size: 14px;
  line-height: 24px;
  /* color: #FFFFFF; */
}
</style>