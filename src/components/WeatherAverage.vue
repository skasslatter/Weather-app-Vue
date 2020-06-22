<template>
  <div class="avarage-temp">
    <div class="date">{{dateString}}</div>
    <div class="temp-container">
      <div class="temp">{{this.averageTemperature}}</div>
      <div class="celsius">°C</div>
    </div>
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
      let average = Math.round(sum / arr.length);
      this.$emit("average", average);
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
        return `${startMonth} ${startDate.day} ${startDate.year} - ${endMonth} ${endDate.day} ${endDate.year}`;
      } else if (startDate.month !== endDate.month) {
        return `${startMonth} ${startDate.day} - ${endMonth} ${endDate.day} ${startDate.year}`;
      } else {
        return `${startMonth} ${startDate.day} - ${endDate.day} ${startDate.year}`;
      }
    }
  }
};
</script>

<style scoped>
.date {
  text-transform: uppercase;
  font-family: Poppins;
  font-style: normal;
  font-weight: 600;
  font-size: 12px;
  line-height: 24px;

  display: flex;
  align-items: center;
  letter-spacing: 0.06em;

  color: #08153e;
  margin-bottom: 27px;
}

.avarage-temp {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.temp-container {
  display: flex;
  margin-bottom: 48px;
}

.temp {
  font-weight: 600;
  font-size: 120px;
  line-height: 120px;

  color: #ffffff;
}

.celsius {
  font-weight: 600;
  font-size: 24px;
  line-height: 32px;

  color: #ffffff;
}
</style>
