<template>
  <div id="app">
    <header
      class="d-flex justify-content-between align-items-center bg-dark px-3"
    >
      <h1 class="text-danger text-uppercase">Boolflix</h1>
      <Searchbar
        placeholder="Search..."
        buttonText="Search"
        @sendResearch="getTitle"
        @newTemplate="getList"
      />
    </header>
    <main v-if="selectedMovie" class="container-fluid">
      <h3 class="mt-5 mb-4 h1 text-white">Movies:</h3>
      <Card :list="movies" class="row" />
      <h3 class="mt-5 mb-4 h1 text-white">Series:</h3>
      <Card :list="series" class="row" />
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
      selectedMovie: "",
      movies: [{}],
      series: [{}],
      api: {
        baseUri: "https://api.themoviedb.org/3",
        key: "a49fd2ad1915c16f5b21a815b7e90362",
      },
    };
  },
  methods: {
    getTitle(userResearch) {
      this.selectedMovie = userResearch;
    },
    getList() {
      this.axiosTemplate("search/movie", "movies");
      this.axiosTemplate("search/tv", "series");
      this.axiosTemplate("search/tv", "series");
      //!https://api.themoviedb.org/3/movie/27205/credits?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=en-US
    },
    axiosTemplate(params, key) {
      axios
        .get(
          `${this.api.baseUri}/${params}?api_key=${this.api.key}&language=it-IT&query=${this.selectedMovie}`
        )
        .then((res) => {
          this[key] = res.data.results;
        })
        .catch((warning) => {
          console.log(warning);
        });
      /*       axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=it-IT&query=${this.selectedMovie}`
        )
        .then((res) => {
          this.series = res.data.results;
        })
        .catch((warning) => {
          console.log(warning);
        }); */
    },
  },
};
</script>

<style lang="scss">
@import "./assets/scss/_style.scss";
</style>
 