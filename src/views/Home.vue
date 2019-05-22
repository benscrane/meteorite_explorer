<template>
  <div>
    <h2 id="header">Meteorite Explorer</h2>
    <SearchBar @search="findMeteorites" />
    <Loader v-show="loading" />
    <SearchResults v-show="!loading" :meteoriteData="meteoriteData" />
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "@/components/SearchBar.vue";
import Loader from "@/components/Loader.vue";
import SearchResults from "@/components/SearchResults.vue";

export default {
  name: "Home",
  components: {
    SearchBar,
    SearchResults,
    Loader
  },
  data() {
    return {
      meteoriteData: [],
      lastSearch: undefined,
      loading: true
    };
  },
  methods: {
    async findMeteorites(e) {
      console.log(e);
      // load data and populate meteorite data array;
      if (e !== this.lastSearch) {
        this.loading = true;
        this.lastSearch = e;
        let url = "https://data.nasa.gov/resource/gh4g-9sfh.json";
        if (e !== "") {
          url += `?$where=name like '%25${e}%25'`;
        }
        let res = await axios.get(url);
        this.meteoriteData = res.data;
        this.loading = false;
      }
    }
  },
  mounted() {
    this.findMeteorites("");
  }
};
</script>

<style scoped>
#header {
  background-color: #122c34;
  color: #f2f3f4;
  padding: 0.5em 0;
  margin-top: 0;
  margin-bottom: 0.75em;
}
</style>
