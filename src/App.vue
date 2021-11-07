<template>
  <div id="app">
    <CovidTable></CovidTable>
  </div>
</template>

<script>
import CovidTable from "@/components/CovidTable";
export default {
  name: 'App',
  components: {
    CovidTable,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
