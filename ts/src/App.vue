<template>
  <div>
    <form id="search">
      Search
      <input name="query" v-model="searchQuery" />
    </form>
    <demo-grid :heroes="gridData" :columns="gridColumns" :filter-key="searchQuery"></demo-grid>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import DemoGrid from "./components/DemoGrid.vue";
import { GridEntry } from "./models/grid-entry.model";

@Component({
  components: {
    DemoGrid
  }
})
export default class App extends Vue {

  private searchQuery = "";

  private gridColumns = ["name", "power"];

  private gridData: GridEntry[] = [
    { name: "Chuck Norris", power: Infinity },
    { name: "Bruce Lee", power: 9000 },
    { name: "Jackie Chan", power: 7000 },
    { name: "Jet Li", power: 8000 }
  ];
}
</script>

<style>
body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}
</style>
