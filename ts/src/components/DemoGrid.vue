<template>
  <table>
    <thead>
      <tr>
        <th
          v-for="key in columns"
          :key="key"
          @click="sortBy(key)"
          :class="{ active: sortKey == key }"
        >
          {{ key | capitalize }}
          <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in filteredHeroes" :key="entry">
        <td v-for="key in columns" :key="key">{{ entry[key] }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { GridEntry } from "../models/grid-entry.model";

type SortOrders = { [key: string]: number };

@Component({
  filters: {
    capitalize(str: string): string {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
})
export default class DemoGrid extends Vue {
  @Prop() heroes!: GridEntry[];
  @Prop() columns!: string[];
  @Prop() filterKey!: string;

  private sortKey: string = '';
  private sortOrders: SortOrders = this.columns.reduce((result: SortOrders, column: string) => {
    result[column] = 1;
    return result;
  }, {});

  private get filteredHeroes(): GridEntry[] {
    const sortKey = this.sortKey;
    const filterKey = this.filterKey && this.filterKey.toLowerCase();
    const order = this.sortOrders[sortKey] || 1;
    let heroes = this.heroes;

    if (filterKey) {
      heroes = heroes.filter(row =>
        Object.keys(row).some(
          key =>
            String(row[key])
              .toLowerCase()
              .indexOf(filterKey) > -1
        )
      );
    }
    if (sortKey) {
      heroes = heroes.slice().sort((a, b) => {
        a = a[sortKey];
        b = b[sortKey];
        return (a === b ? 0 : a > b ? 1 : -1) * order;
      });
    }
    return heroes;
  }

  private sortBy(key: string): void {
    this.sortKey = key;
    this.sortOrders[key] = this.sortOrders[key] * -1;
  }
}
</script>

<style scoped>
table {
  border: 2px solid #42b983;
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

th.active {
  color: #fff;
}

th.active .arrow {
  opacity: 1;
}

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}
</style>
