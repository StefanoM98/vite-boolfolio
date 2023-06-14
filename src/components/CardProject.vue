<script>
import { store } from "../store";
export default {
  name: "CardProjects",
  props: {
    project: Object,
  },
  data() {
    return {
      store,
    };
  },
  computed: {
    getImgurl() {
      return this.store.baseUrl + "/storage/" + this.project.image;
    },
  },
};
</script>

<template>
  <div class="card h-100">
    <img v-if="project.image" :src="getImgurl" alt="" />
    <div v-else>Nessuna immagine caricata</div>
    <div class="card-body">
      {{ project.title }}
    </div>
  </div>
</template>
