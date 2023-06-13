<script>
import axios from "axios";
import CardProject from "./components/CardProject.vue";
export default {
  data() {
    return {
      baseUrl: "http://localhost:8000",
      projects: [],
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects() {
      axios.get(`${this.baseUrl}/api/projects`).then((resp) => {
        this.projects = resp.data.results;
      });
    },
  },
  components: {
    CardProject,
  },
};
</script>

<template>
  <div class="container">
    <h1>Lista dei Progetti</h1>
    <div class="row row-cols-3 g-4">
      <div class="col" v-for="project in projects" :key="project.id">
        <CardProject :project="project" />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
