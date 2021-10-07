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
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: "Open Sans", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #D7D7D7;
}
</style>
