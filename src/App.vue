<script>
import AppHeader from './components/AppHeader.vue';
import AppFilms from "./components/AppFilms.vue";
import AppTv from './components/AppTv.vue';
import { store } from "./store";
import axios from 'axios';
export default {
  components: {
    AppHeader,
    AppFilms,
    AppTv
  },
  data() {
    return {
      store
    }
  },
  methods: {
    search_title() {
      store.arrayFilms = []
      axios.get(`${store.urlFilms}${store.APIKey}&query=${store.searchValue}&language=it-IT`).then(response => {
        store.arrayFilms = [...response.data.results];
      })
      store.arrayTv = []
      axios.get(`${store.urlTv}${store.APIKey}&language=it-IT&query=${store.searchValue}`).then(data => {
        store.arrayTv = [...data.data.results];
        console.log(store.arrayTv);
      })
    }
  },
}
</script>
<template lang="">
  <AppHeader @SearchTitle="search_title"/>
  <div class="container">
    <AppFilms/>
    <AppTv/>
  </div>
</template>
<style lang="scss">
@use './styles/generals.scss';
</style>