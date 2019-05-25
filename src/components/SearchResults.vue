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
        v-for="meteorite in meteoriteList"
        :key="meteorite.id"
        :meteorite="meteorite"
      />
      <tr v-if="meteoriteData.length == 0 && !error">
        <td colspan="9">
          No matching meteorite results
        </td>
      </tr>
      <tr v-if="error">
        <td colspan="9">
          Something went wrong, try again in a few seconds
        </td>
      </tr>
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
    },
    error: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    meteoriteList() {
      if (!this.error) {
        return this.meteoriteData;
      } else {
        return [];
      }
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
  background-color: #fdca40;
  border: none;
}
th,
td {
  padding: 0.6em;
  font-size: 1.2em;
}
td {
  text-align: center;
}
</style>
