<template>
  <div>
    <h2>Meteorite Explorer</h2>
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
