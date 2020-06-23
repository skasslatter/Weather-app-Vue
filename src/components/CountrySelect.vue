<template>
  <div>
    <div class="flag-container">
      <img :src="flagUrl" alt="flag" class="flag" />
      <!-- <div class="flag" v-bind:style="flagUrl" /> -->
    </div>

    <select
      name="countries"
      class="countries"
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
    >
      <option v-for="(country, index) in countries" :key="index" :value="country.key">
        <!-- {{country.flag}} -->
        {{country.key}}
      </option>
    </select>
  </div>
</template>

<script>
import { countries } from "countries-list";
const countriesNameAndFlag = [];
for (const key in countries) {
  countriesNameAndFlag.push({
    key: key,
    flag: countries[key].emoji
  });
}

export default {
  name: "CountrySelect",
  props: ["value"],
  data() {
    return {
      countries: countriesNameAndFlag
    };
  },
  computed: {
    flagUrl: function() {
      // return `background-image: url(https://www.countryflags.io/${this.value}/flat/64.png); background-repeat: no-repeat; width: 100%;height: 100%;`;
      // return `background: red`
      return `https://www.countryflags.io/${this.value}/flat/64.png`;
    }
  }
};
</script>

<style scoped>
.countries {
  border-width: 0px;
  outline: none;
  font-family: Poppins;
  font-weight: 600;
  color: #08153e;
}

select {
  -webkit-appearance: none;
  -moz-appearance: none;
  background: transparent;
  background-image: url("data:image/svg+xml;utf8,<svg fill='gray' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/><path d='M0 0h24v24H0z' fill='none'/></svg>");
  background-repeat: no-repeat;
  background-position-x: 36px;
  background-position-y: 8px;
  border: 1px solid #dfdfdf;
  width: 100%;
  display: flex;
  padding: 10px 15px;
}

.flag-container {
  min-width: 18px;
  height: 14px;
  overflow: hidden;
  border: 1px solid #08153e;
  box-sizing: border-box;
  border-radius: 3px;
}

.flag {
  width: 20px;
  height: 22px;
  top: -5px;
  left: -2px;
  position: relative;
}
</style>
