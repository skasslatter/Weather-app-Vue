<template>
  <div id="app">
    <SearchBar />
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar";

export default {
  name: "App",
  components: {
    SearchBar
  },
  methods: {
    getWeather() {
      console.log("testing getWeather ");
      axios
        .get(`http://api.weatherbit.io/v2.0/current&key=${process.env.APIKEY}&city=Raleigh&country=US`)
        .then(response => {
          console.log("response: ", response);
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

