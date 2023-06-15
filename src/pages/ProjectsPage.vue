<script>
import axios from "axios";
import { store } from "../store";
import CardProject from "../components/CardProject.vue";
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
  },
};
</script>
<template>
  <h1>My ProjectsPage</h1>

  <div class="container">
    <section v-if="!load">
      <h1>Lista dei Progetti</h1>
      <div class="row row-cols-5 g-4">
        <div class="col" v-for="project in projects">
          <CardProject :project="project" />
        </div>
      </div>
      <nav class="mt-4">
        <ul class="pagination">
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <a
              @click.prevent="getProjects(currentPage - 1)"
              class="page-link"
              href="#"
            >
              Previous
            </a>
          </li>
          <li
            class="page-item"
            v-for="pageNumber in lastPage"
            :class="{ active: pageNumber === currentPage }"
          >
            <a
              @click.prevent="getProjects(pageNumber)"
              class="page-link"
              href="#"
            >
              {{ pageNumber }}
            </a>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === lastPage }">
            <a
              @click.prevent="getProjects(currentPage + 1)"
              class="page-link"
              href="#"
            >
              Next
            </a>
          </li>
        </ul>
      </nav>
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
