<template>
  <div>
    <h2>Meteorite Explorer</h2>
    <SearchBar />
  </div>
</template>

<script>
import SearchBar from "@/components/SearchBar.vue";

export default {
  name: "Home",
  components: {
    SearchBar
  }
};
</script>
