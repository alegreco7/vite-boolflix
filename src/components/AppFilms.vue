<script>
import AppVote from "./AppVote.vue";
import { store } from "../store";
export default {
    components: {
        AppVote
    },
    data() {
        return {
            store,
        }
    },
    methods: {
        getFlag(lang) {
            let src = ''
            if (lang == 'en') {
                src = `https://flagsapi.com/GB/flat/64.png`
                return src
            }
            src = `https://flagsapi.com/${lang.toUpperCase()}/flat/64.png`
            return src
        },
        getImage(img) {
            let string = '';
            if (img == null) {
                string = '/src/assets/img/no-image.jpg';
                return string
            }
            string = `http://image.tmdb.org/t/p/w500${img}`;
            return string;
        }
    },
}
</script>
<template lang="">
    <div class="row my-3 g-2">
        <div class="col-12">
            <h1>Film</h1>
        </div>
        <div class="col-4 col-md-3 col-lg-2" v-for="(film, index) in store.arrayFilms" :key="index">
            <div class="info">
                <div class="thumb">
                    <img :src="getImage(film.poster_path)" :alt="film.title">
                </div>
                <div class="content">
                    <div class="title">
                        <h4>{{ film.title }}</h4>
                        <span class="subtitle">{{ film.original_title }}</span>
                        <AppVote :vote_value="film.vote_average"/>
                        
                    </div>
                    <div class="description">
                        <h6>Descrizione:</h6>
                        <p>
                            {{ film.overview }}
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style lang="scss" scoped>
@use '../styles/generals.scss';
@use '../styles/movies.scss';
</style>