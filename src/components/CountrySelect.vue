<template>
  <div>
    <!-- <label for="countries">Choose a country:</label> -->
    <select name="countries" 
      v-bind:value="value"
      v-on:input="$emit('input', $event.target.value)"
      >
      <option
        v-for="(country, index) in countries"
        :key="index"
        :value="country.key"
      >{{country.flag}} {{country.key}}</option>
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
  props: ['value'],
  data() {
    return {
      countries: countriesNameAndFlag
    };
  }
};
</script>

<style scoped>
</style>
