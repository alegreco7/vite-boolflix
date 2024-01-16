<script>
import AppHeader from './components/AppHeader.vue';
import AppHome from './components/AppHome.vue';
import AppSearched from './components/AppSearched.vue';

import { store } from "./store";
import axios from 'axios';
export default {
  components: {
    AppHeader,
    AppHome,
    AppSearched
  },
  data() {
    return {
      store
    }
  },
  created() {
    this.getHome()
  },
  methods: {
    search_title() {
      if (store.searchValue != '') {
        store.searched = true;
      } else {
        store.searched = false;
      }
      store.arrayFilms = []
      axios.get(`${store.urlFilms}${store.APIKey}&query=${store.searchValue}&language=it-IT`).then(response => {
        store.arrayFilms = response.data.results;
      })
      store.arrayTv = []
      axios.get(`${store.urlTv}${store.APIKey}&language=it-IT&query=${store.searchValue}`).then(data => {
        store.arrayTv = data.data.results;
      })
    },
    getHome() {
      store.popularFilms = [];
      store.popularSeries = [];
      axios.get(`${store.urlPopularFilms}${store.APIKey}&language=it-IT`).then(result => {
        store.popularFilms = result.data.results;
      })
      axios.get(`${store.urlPopularTV}${store.APIKey}&language=it-IT`).then(res => {
        store.popularSeries = res.data.results;
      })
    }
  },
}
</script>
<template lang="">
  <AppHeader @SearchTitle="search_title"/>
  <AppSearched/>
  <AppHome/>
</template>
<style lang="scss">
@use './styles/generals.scss';
</style>