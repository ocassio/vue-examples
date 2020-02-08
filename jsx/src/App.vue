<script>
import DemoGrid from "./components/DemoGrid.vue";

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
  }),
  methods: {
      onSearchChange(e) {
          this.searchQuery = e.target.value;
      }
  },
  render() {
      return (
          <div>
            <form id="search">
                Search
                <input
                    name="query"
                    value={this.searchQuery}
                    on-input={this.onSearchChange} />
            </form>
            <demo-grid
                heroes={this.gridData}
                columns={this.gridColumns}
                filterKey={this.searchQuery}>
            </demo-grid>
          </div>
      );
  }
};
</script>

<style>
body {
  font-family: Helvetica Neue, Arial, sans-serif;
  font-size: 14px;
  color: #444;
}
</style>
