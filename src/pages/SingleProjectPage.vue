<script>
import axios from "axios";
import { store } from "../store";
export default {
  name: "SingleProjectPage",
  data() {
    return {
      store,
      project: null,
    };
  },
  mounted() {
    const slug = this.$route.params.slug;
    axios.get(`${this.store.baseUrl}/api/projects/${slug}`).then((resp) => {
      this.project = resp.data.results;
    });
  },
};
</script>
<template>
  <div class="container">
    <h1 class="m-4">My SingleProjectPage</h1>
    <div v-if="project">
      <h3>{{ project.title }}</h3>
      <div>
        <img
          v-if="project.image"
          :src="`${store.baseUrl}/storage/${project.image}`"
          alt=""
        />
        <h4 v-else>Nessuna immagine presente</h4>
      </div>
    </div>
    <div v-else>Errore</div>
  </div>
</template>

<style lang="scss" scoped></style>
