<template>
  <div>
    <form v-on:submit.prevent="findMeteorites">
      <input
        v-model="searchText"
        type="text"
        placeholder="Enter search terms"
      />
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
}
button {
  text-transform: uppercase;
}
</style>
