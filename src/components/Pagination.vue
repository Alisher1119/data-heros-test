<template>
  <div class="pagination">
    <button @click="onPageChange(currentPage - 1)" :disabled="!(currentPage > 1)"><</button>
    <button v-for="index in params.pages" @click="onPageChange(index)" :disabled="currentPage === index">
      {{index}}
    </button>
    <button @click="onPageChange(currentPage + 1)" :disabled="!(currentPage < params.pages)">></button>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";

const props = defineProps(['params']);
const emits = defineEmits(['pageChange']);

const currentPage = ref(1);
const onPageChange = (page = 1) => {
  currentPage.value = page;
  emits('pageChange', {page});
}
console.log(props.params, currentPage.value)

</script>

<style scoped lang="scss">
.pagination {
  padding: 1.5rem;

  button {
    padding: 0.3rem 0.5rem;
    margin: 0.1rem;
  }
}
</style>
