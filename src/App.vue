<template>
  <div id="app">
    <header
      class="d-flex justify-content-between align-items-center bg-dark px-3"
    >
      <h1 class="text-danger text-uppercase">Boolflix</h1>
      <Searchbar @sendTitle="getTitle" @newTemplate="axiosTemplate" />
    </header>
    <main>
      <h3>Movies</h3>
      <Card :list="moviesList" />
      <h3>Series</h3>
      <Card :list="seriesList" />
    </main>
  </div>
</template>

<script>
import Searchbar from "./components/Searchbar.vue";
import Card from "./components/Card.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Searchbar,
    Card,
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
    /*     getFlag(language) {
      if (language == "en") {
        return require(`./assets/images/en.png`);
      } else if (language == "it") {
        return require(`./assets/images/it.png`);
      } else {
        return;
      }
    }, */
    /*     getAverage(average) {
      return Math.ceil(average % 2);
    }, */
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
