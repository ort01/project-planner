<template>
  <div v-if="projects.length" class="home">
    <FilterNav
      @filterChange="currentFilter = $event"
      :currentFilter="currentFilter"
    />
    <!-- accesing the data "by" we sent through this.$emit("filterChange", by) with $event => $event = by -->
    <div v-for="project in projects" :key="project.id">
      <SingleProject
        :project="project"
        @delete="handleDelete"
        @complete="handleComplete"
      />
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: "Home",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      currentFilter: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((error) => console.log(error.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((item) => {
        return item.id !== id;
      });
    },
    handleComplete(id) {
      var foundProject = this.projects.find((item) => {
        return item.id === id;
      });
      foundProject.complete = !foundProject.complete;
    },
  },
  computed: {
    filtteredObjects() {},
  },
};
</script>
