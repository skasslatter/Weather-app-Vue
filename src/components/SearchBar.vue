<template>
  <div class="searchbar">
    <img class="cloud-icon" src="/cloud.png" alt="Cloud" />
    <CountrySelect v-model="countryCode" class="country-select" />
    <div class="search-text">
      <input
        v-model="location"
        v-on:keyup.enter="handleSubmit"
        type="text"
        placeholder="Please enter your location..."
      />
      <img
        v-on:click="handleSubmit"
        src="/magnifyingGlass.png"
        alt="Search"
        :class="!location  ? 'transparent' : ''"
      />
    </div>
  </div>
</template>

<script>
import CountrySelect from "./CountrySelect";

export default {
  name: "SearchBar",
  data() {
    return {
      location: "",
      countryCode: "NL"
    };
  },
  components: {
    CountrySelect
  },
  methods: {
    handleSubmit() {
      console.log("testing handleSubmit: ", this.location, this.countryCode);
      let data = {
        location: this.location,
        countryCode: this.countryCode
      };
      this.$emit("search", data);
    }
  }
};
</script>

<style scoped>
.searchbar {
  width: 588px;
  background: linear-gradient(
      0deg,
      rgba(255, 255, 255, 0.9),
      rgba(255, 255, 255, 0.9)
    ),
    #f8f8f8;
  box-shadow: 0px 2px 10px rgba(8, 21, 62, 0.15);
  border-radius: 16px;
  display: flex;
  justify-content: space-around;
  margin-bottom: 48px;
  padding: 22px;
}

.cloud-icon {
  width: 48px;
  height: 48px;
  align-self: center;
}

.search-text {
  width: 391px;
  border: 1px solid rgba(8, 21, 62, 0.05);
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 9px 17px;
}

.search-text:hover {
  border: 1px solid #b5c7ff;
}

.search-text:focus-within {
  border: 2px solid #b5c7ff;
  padding: 8px 16px;
}

.search-text input {
  width: 299px;
  height: 30px;
  padding: 0px;
  /* font-weight: normal;
  font-size: 14px;
  line-height: 21px;
  display: flex;
  align-items: center; */
  color: #08153e;
  border-width: 0;
  outline: none;
}

/* .search-text img {
  width: 17.41px;
  height: 19.41px;
  left: 981px;
  top: 410px;
} */

.country-select {
  width: 80px;
  height: 48px;
  border: 1px solid rgba(8, 21, 62, 0.05);
  border-radius: 6px;
  display: flex;
  align-items: center;
  padding-left: 15px;
}

.transparent {
  opacity: 0.5;
}
</style>

