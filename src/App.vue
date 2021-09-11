<template>
  <div id="app">
    <header
      class="d-flex justify-content-between align-items-center bg-dark px-3"
    >
      <h1 class="text-danger text-uppercase">Boolflix</h1>
      <Searchbar @sendTitle="getTitle" @newTemplate="axiosTemplate" />
    </header>
    <main>
      <h3>Film</h3>
      <ul class="">
        <li class="mb-3" v-for="movie in moviesList" :key="movie.id">
          <ul>
            <li>Title: {{ movie.title }}</li>
            <li>Original title: {{ movie.original_title }}</li>
            <li>Original language: {{ movie.original_language }}</li>
            <li>Rating: {{ movie.vote_average }}</li>
          </ul>
        </li>
      </ul>
      <h3>Serie</h3>
      <ul>
        <li class="mb-3" v-for="serie in seriesList" :key="serie.id">
          <ul>
            <li>Title: {{ serie.name }}</li>
            <li>Original title: {{ serie.original_name }}</li>
            <li>Original language: {{ serie.original_language }}</li>
            <li>Rating: {{ serie.vote_average }}</li>
          </ul>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
import Searchbar from "./components/Searchbar.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Searchbar,
  },
  data() {
    return {
      selectedMovie: "up",
      moviesList: [{}],
      seriesList: [{}],
    };
  },
  methods: {
    getTitle(userTitle) {
      this.selectedMovie = userTitle;
    },
    axiosTemplate() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=it-IT&query=${this.selectedMovie}`
        )
        .then((res) => {
          this.moviesList = res.data.results;
        })
        .catch((warning) => {
          console.log(warning);
        });
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=it-IT&query=${this.selectedMovie}`
        )
        .then((res) => {
          this.seriesList = res.data.results;
        })
        .catch((warning) => {
          console.log(warning);
        });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/scss/_style.scss";
</style>
