<script>
export default {
  name: "Pagination",
  props: {
    currentPage: Number,
    lastPage: Number,
  },
  emits: ["changePage"],
};
</script>
<template>
  <nav class="m-4">
    <ul class="pagination">
      <li class="page-item" :class="{ disabled: currentPage === 1 }">
        <a
          @click.prevent="$emit('changePage', currentPage - 1)"
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
          @click.prevent="$emit('changePage', pageNumber)"
          class="page-link"
          href="#"
        >
          {{ pageNumber }}
        </a>
      </li>
      <li class="page-item" :class="{ disabled: currentPage === lastPage }">
        <a
          @click.prevent="$emit('changePage', currentPage + 1)"
          class="page-link"
          href="#"
        >
          Next
        </a>
      </li>
    </ul>
  </nav>
</template>

<style lang="scss" scoped></style>
