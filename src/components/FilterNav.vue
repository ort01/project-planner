<template>
  <nav class="filter-nav">
    <button
      @click="updateFilter('all')"
      :class="{ active: currentFilter === 'all' }"
    >
      View All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: currentFilter === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: currentFilter === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  name: "FilterNav",
  props: ["currentFilter"],
  data: () => {
    return {};
  },
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
    },
  },
};
</script>


<style scoped>
.filter-nav button {
  border: none;
  outline: none;
  background: none;
  color: #bbb;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-right: 10px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>