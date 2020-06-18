<template>
  <div class="searchbar">
    <img class="cloud-icon" src="/cloud.png" alt="Cloud" />
    <CountrySelect v-model="countryCode" />
    <div class="search-text">
      <input
        v-model="location"
        v-on:keyup.enter="handleSubmit"
        type="text"
        placeholder="Please enter your location.."
      />
      <img src="magnifyingGlass.png" alt="Magnifying Glass" />
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
  position: absolute;
  width: 632px;
  height: 92px;
  left: 404px;
  top: 374px;
  background: linear-gradient(
      0deg,
      rgba(255, 255, 255, 0.9),
      rgba(255, 255, 255, 0.9)
    ),
    #f8f8f8;
  box-shadow: 0px 2px 10px rgba(8, 21, 62, 0.15);
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.cloud-icon {
  /* position: absolute; */
  width: 48px;
  height: 48px;
  left: 426px;
  top: 396px;
  align-self: center;
}

.search-text {
  width: 425px;
  height: 48px;
  left: 589px;
  top: 396px;

  background: #ffffff;
  border: 1px solid rgba(8, 21, 62, 0.05);
  border-radius: 6px;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.search-text input {
  width: 299px;
  height: 30px;
  left: 606px;
  top: 405px;

  font-family: Poppins;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 21px;
  display: flex;
  align-items: center;

  color: #08153e;
  opacity: 0.5;
  border-width: 0;
}

.search-text img {
  width: 17.41px;
  height: 19.41px;
  left: 981px;
  top: 410px;
}
</style>
