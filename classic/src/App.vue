<template>
  <div>
    <form id="search">
      Search
      <input name="query" v-model="searchQuery" />
    </form>
    <demo-grid :heroes="gridData" :columns="gridColumns" :filter-key="searchQuery"></demo-grid>
  </div>
</template>

<script>
import DemoGrid from "./components/DemoGrid";

export default {
  name: "app",
  components: {
    DemoGrid
  },
  data: () => ({
    searchQuery: "",
    gridColumns: ["name", "power"],
    gridData: [
      { name: "Chuck Norris", power: Infinity },
      { name: "Bruce Lee", power: 9000 },
      { name: "Jackie Chan", power: 7000 },
      { name: "Jet Li", power: 8000 }
    ]
  })
};
</script>

<style>
body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}
</style>
