<template>
  <div>
    <h2 id="header">Meteorite Explorer</h2>
    <SearchBar @search="findMeteorites" :previousSearches="previousSearches" />
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
      loading: true,
      previousSearches: []
    };
  },
  methods: {
    async findMeteorites(e) {
      // load data and populate meteorite data array;
      if (e !== this.lastSearch) {
        this.loading = true;
        this.lastSearch = e;
        this.updateSearchHistory(e);
        let url = "https://data.nasa.gov/resource/gh4g-9sfh.json";
        if (e !== "") {
          url += `?$where=UPPER(name) like '%25${e.toUpperCase()}%25'`;
        }
        let res = await axios.get(url);
        this.meteoriteData = res.data;
        this.loading = false;
      }
    },
    updateSearchHistory(searchTerm) {
      if (searchTerm !== "") {
        if (this.previousSearches.includes(searchTerm)) {
          // remove previous search term
          this.previousSearches.splice(
            this.previousSearches.indexOf(searchTerm),
            1
          );
        }
        this.previousSearches.unshift(searchTerm);
      }
      if (this.previousSearches.length > 10) {
        this.previousSearches.pop();
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
