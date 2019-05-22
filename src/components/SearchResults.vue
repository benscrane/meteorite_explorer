<template>
  <div id="table">
    <table cellspacing="0">
      <tr id="header">
        <th width="20%">Name</th>
        <th width="5%">Id</th>
        <th width="10%">Name Type</th>
        <th width="12%">Rec Class</th>
        <th width="10%">Mass (g)</th>
        <th width="10%">Fall</th>
        <th width="13%">Year</th>
        <th width="10%">Latitude</th>
        <th width="10%">Longitude</th>
      </tr>
      <Meteorite
        v-for="meteorite in meteoriteData"
        :key="meteorite.id"
        :meteorite="meteorite"
      />
    </table>
  </div>
</template>

<script>
import Meteorite from "@/components/Meteorite.vue";

export default {
  name: "SearchResults",
  components: {
    Meteorite
  },
  props: {
    meteoriteData: {
      type: Array,
      default: () => []
    }
  }
};
</script>

<style scoped>
* {
  text-align: start;
}
#table {
  margin: 4vh auto;
  display: flex;
  flex-direction: column;
  width: 90vw;
  background-color: white;
}
#table table {
  width: 100%;
}
#header {
  background-color: lightblue;
  border: none;
}
#header th {
  padding: 0.5em;
  font-size: 1.2em;
}
</style>
