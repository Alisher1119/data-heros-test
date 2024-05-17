<template>
  <form @submit.prevent="onSubmit($event)">
    <input name="name">
    <select name="status">
      <option value="" selected disabled></option>
      <option value="alive" >Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button type="submit">Применить</button>
    <button type="reset">Reset</button>
  </form>

</template>

<script setup lang="ts">

const emits = defineEmits<{ filter: [{name: string, status: string}] }>();

const onSubmit = ($e: any) => {
  const data = new FormData($e.target);

  let params = {
    name: '',
    status: '',
    page: 1,
  };

  for (const [key, value] of data.entries()) {
    params = {
      ...params,
      [key]: value,
      page: 1,
    };
  }

  emits('filter', params);
}
</script>
