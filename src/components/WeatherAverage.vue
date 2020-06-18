<template>
  <div>Average is {{this.averageTemperature}}</div>
</template>

<script>
export default {
  name: "WeatherForecast",
  data() {
    return {
    };
  },
  components: {},
  methods: {
  },
  props: {
    forecastData: Array
  },
  computed: {
    averageTemperature: function () {
      if (!this.forecastData) {
        return null
      }
      let arr = [];
      for (let i = 0; i < this.forecastData.length; i++) {
        arr.push(this.forecastData[i].temp);
      }
      let sum = 0;
      for (let i = 0; i < arr.length; i++) {
        sum = sum + i;
      }
      let average = sum / arr.length;
      return average
    }
  }
};
</script>

<style scoped>
</style>
