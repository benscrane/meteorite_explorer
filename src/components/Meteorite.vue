<template>
  <tr>
    <td>{{ meteorite.name }}</td>
    <td>{{ meteorite.id }}</td>
    <td>{{ meteorite.nametype }}</td>
    <td>{{ meteorite.recclass }}</td>
    <td>{{ meteorite.mass }}</td>
    <td>{{ meteorite.fall }}</td>
    <td>{{ new Date(meteorite.year).getFullYear() }}</td>
    <td>
      {{
        meteorite.geolocation
          ? Number.parseFloat(meteorite.geolocation.latitude).toFixed(6)
          : ""
      }}
    </td>
    <td>
      {{
        meteorite.geolocation
          ? Number.parseFloat(meteorite.geolocation.longitude).toFixed(6)
          : ""
      }}
    </td>
  </tr>
</template>

<script>
export default {
  name: "Meteorite",
  props: {
    meteorite: {
      type: Object,
      default: () => {}
    }
  }
};
</script>

<style scoped>
td {
  padding: 0.5em;
  font-size: 1.2em;
  border-bottom: thin solid grey;
  background-color: #f2f3f4;
}
</style>
