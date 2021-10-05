<template>
  <div id="app">
    <filter-flights />
  </div>
</template>

<script>
import FilterFlights from "./views/FilterFlights.vue";

export default {
  name: "App",
  components: {
    FilterFlights,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
