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
  padding: 0.4em;
  border: none;
}
button {
  text-transform: uppercase;
  background-color: #122c34;
  color: white;
}
</style>
