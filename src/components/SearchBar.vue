<template>
  <div>
    <form v-on:submit.prevent="findMeteorites">
      <input
        v-model="searchText"
        type="search"
        list="searchHistory"
        placeholder="Enter search terms"
      />
      <datalist id="searchHistory">
        <option
          v-for="(search, i) in previousSearches"
          :key="i"
          :value="search"
        />
      </datalist>
      <button>Search</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  data() {
    return {
      searchText: ""
    };
  },
  props: {
    previousSearches: {
      type: Array
    }
  },
  methods: {
    findMeteorites() {
      this.$emit("search", this.searchText);
    }
  }
};
</script>

<style scoped>
* {
  font-size: 1.1em;
  padding: 0.4em;
  border: none;
}
input {
  background-color: #f2f3f4;
}
button {
  text-transform: uppercase;
  background-color: #122c34;
  color: #f2f3f4;
}
</style>
