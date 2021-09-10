<template>
  <div id="app">
    <header
      class="d-flex justify-content-between align-items-center bg-dark px-3"
    >
      <h1 class="text-danger text-uppercase">Boolflix</h1>
      <Searchbar @sendTitle="getTitle" />
    </header>
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
      moviesList: {},
    };
  },
  methods: {
    getTitle(userTitle) {
      this.selectedMovie = userTitle;
    },
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/search/movie?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=it-IT&query=${this.selectedMovie}`
      )
      .then((res) => {
        this.moviesList = res;
      })
      .catch((warning) => {
        console.log(warning);
      });
  },
};
</script>

<style lang="scss">
@import "./assets/scss/_style.scss";
</style>
