<script>
export default {
  name: "CardProjects",
  props: {
    project: Object,
  },
  data() {
    return {
      baseUrl: "http://localhost:8000",
    };
  },
};
</script>

<template>
  <div class="card h-100">
    <img
      v-if="project.image"
      :src="`${baseUrl}/storage/${project.image}`"
      alt=""
    />
    <div v-else>Nessuna immagine caricata</div>
    <div class="card-body">
      {{ project.title }}
    </div>
  </div>
</template>
