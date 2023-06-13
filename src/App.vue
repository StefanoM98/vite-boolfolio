<script>
import axios from "axios";
import { store } from "./store";
export default {
  data() {
    return {
      store,
    };
  },
  mounted() {},
  methods: {
    getProjects() {
      axios.get(store.baseUrl).then((resp) => {
        store.projects = resp.data;
      });
    },
  },
};
</script>

<template>
  <div class="container">
    <h1>Lista dei Progetti</h1>
    <div class="row row-cols-4 g-4"></div>
  </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
