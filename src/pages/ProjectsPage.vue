<script>
import axios from "axios";
import { store } from "../store";
import CardProject from "../components/CardProject.vue";
import Pagination from "../components/Pagination.vue";

export default {
  name: "ProjectsPage",
  data() {
    return {
      store,
      projects: [],
      currentPage: 1,
      lastPage: null,
      totalProject: 0,
      load: false,
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects(pageNumber = 1) {
      this.load = true;
      axios
        .get(`${this.store.baseUrl}/api/projects`, {
          params: {
            page: pageNumber,
          },
        })
        .then((resp) => {
          this.projects = resp.data.results.data;
          this.currentPage = resp.data.results.current_page;
          this.lastPage = resp.data.results.last_page;
          this.totalProject = resp.data.results.total;
        })
        .finally(() => {
          this.load = false;
        });
    },
  },
  components: {
    CardProject,
    Pagination,
  },
};
</script>
<template>
  <div class="container">
    <section v-if="!load">
      <h1>My ProjectsPage</h1>

      <div class="row row-cols-5 g-4">
        <div class="col m-4" v-for="project in projects">
          <CardProject :project="project" />
        </div>
      </div>
      <Pagination
        @changePage="getProjects"
        :currentPage="currentPage"
        :lastPage="lastPage"
      />
    </section>
    <section v-else>
      <div class="d-flex justify-content-center">
        <div class="spinner-border" role="status">
          <span class="visually-hidden">Loading...</span>
        </div>
      </div>
    </section>
  </div>
</template>

<style lang="scss" scoped></style>
