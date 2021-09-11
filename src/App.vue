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
      <ul class="series-list">
        <li class="mb-3" v-for="serie in seriesList" :key="serie.id">
          <ul>
            <li>Title: {{ serie.name }}</li>
            <li>Original title: {{ serie.original_name }}</li>
            <li>
              Original language:
              <div class="flag-box" v-if="getFlag(serie.original_language)">
                <img
                  class="img-fluid"
                  :src="getFlag(serie.original_language)"
                  :alt="serie.original_language"
                />
              </div>
              <span v-if="!getFlag(serie.original_language)">{{
                serie.original_language
              }}</span>
            </li>
            <li>
              Average: {{ getAverage(serie.vote_average) }}
              <i
                :class="
                  getAverage(serie.vote_average) < 1
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(serie.vote_average) < 2
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(serie.vote_average) < 3
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(serie.vote_average) < 4
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(serie.vote_average) < 5
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
            </li>
          </ul>
          <ul>
            <li>
              <img
                :src="`https://image.tmdb.org/t/p/w342/${serie.poster_path}`"
                :alt="`${serie.title}-cover`"
              />
            </li>
          </ul>
        </li>
      </ul>
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
