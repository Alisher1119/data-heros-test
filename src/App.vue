<template>
  <div class="header">
    <h1>
      Total characters: {{ info.count }}
    </h1>
    <div class="filter">
      <Filters v-on:filter="fetchData($event)"/>
    </div>
  </div>
  <Pagination :params="info" v-on:pageChange="fetchData($event)"/>
  <div class="wrapper">
    <div v-if="errorMessage">
      {{ errorMessage }}
    </div>
    <div v-if="items.length > 0" class="row">
      <Card v-for="item in items" :item="item"/>
    </div>
  </div>

  <Pagination :params="info" v-on:pageChange="fetchData($event)"/>
</template>

<script setup lang="ts">
import {reactive, ref} from "vue";
import type {CharacterInterface} from "@/interfaces/character.interface";
import axios from "axios";
import type {InfoInterface} from "@/interfaces/info.interface";
import Card from "@/components/Card.vue";
import Pagination from "@/components/Pagination.vue";
import Filters from "@/components/Filters.vue";

const defaultApi = 'https://rickandmortyapi.com/api/character';
const defaultInfo: InfoInterface = {
  count: 0,
  pages: 0,
  next: null,
  prev: null,
}

const items = ref<CharacterInterface[]>([]);
const info = ref<InfoInterface>(defaultInfo);
const errorMessage = ref<string>('');

let defaultParams = reactive({
  page: 1,
  name: '',
  status: '',
});

const fetchData = (params = {}) => {

  defaultParams = {
    ...defaultParams,
    ...params
  }

  axios.get(defaultApi, {params: defaultParams}).then((response) => {
    items.value = response.data?.results || [];
    info.value = response.data?.info || defaultInfo;
    errorMessage.value = '';
  }).catch(error => {
    items.value = [];
    info.value = defaultInfo;
    errorMessage.value = error.response.data.error;
  });
}

fetchData(defaultParams);

</script>
