<template>
  <section>
    <div
      class="card-structure position-relative m-4"
      v-for="element in list"
      :key="element.id"
    >
      <ul class="card-list position-absolute bg-dark text-white px-4">
        <li class="mb-3">
          <ul>
            <li>{{ getGenres(element.genre_ids) }}</li>
            <li>
              Title:
              <span v-if="element.title">{{
                element.title || element.name
              }}</span>
              <span v-else>{{ element.name }}</span>
            </li>
            <li>
              Original title:
              <span v-if="element.original_title">{{
                element.original_title
              }}</span>
              <span v-else>{{ element.original_name }}</span>
            </li>
            <li>
              Original language:
              <div class="flag-box" v-if="getFlag(element.original_language)">
                <img
                  class="img-fluid"
                  :src="getFlag(element.original_language)"
                  :alt="element.original_language"
                />
              </div>
              <span v-if="!getFlag(element.original_language)">{{
                element.original_language
              }}</span>
            </li>
            <li>
              <i
                v-for="(star, index) in 5"
                :key="index"
                :class="
                  getAverage(star, index)
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
            </li>
            <li><Actors :id="element.id" :endpoint="params" /></li>
            <li>{{ element.overview }}</li>
          </ul>
        </li>
      </ul>
      <img
        v-if="element.poster_path"
        class="cover position-absolute"
        :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`"
        :alt="`${element.title}-cover`"
      />
      <img
        class="cover h-100"
        v-else
        src="https://www.altavod.com/assets/images/poster-placeholder.png"
        alt="missing-image-placeholder"
      />
    </div>
  </section>
</template>

<script>
import Actors from "../components/Actors.vue";
export default {
  name: "card",
  props: ["params", "list", "genresList"],
  data() {
    return {};
  },
  components: {
    Actors,
  },
  methods: {
    getGenres(currentGenres) {
      if (!currentGenres) return;

      let genresArray = [];
      for (let i = 0; i < currentGenres.length; i++) {
        this.genresList.forEach((element) => {
          if (element.id == currentGenres[i]) {
            genresArray.push(element.name);
          }
        });
      }
      return genresArray;
    },
    getFlag(language) {
      if (language == "en") {
        return require(`../assets/images/en.png`);
      } else if (language == "it") {
        return require(`../assets/images/it.png`);
      } else {
        return;
      }
    },
    getAverage(item, index) {
      const average = Math.ceil(item / 2);
      if (average < index) {
        return true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.card-structure {
  width: 342px;
  height: 513px;
  ul.card-list {
    height: 100%;
    width: 100%;
    border: 3px solid #fff;
    overflow: auto;
    z-index: 1;
    opacity: 0;
    &:hover {
      opacity: 1;
      //?AGGIUNGERE CHE CON IL CLICK LA CARTA SI GIRA E MOSTRA IL RETRO.
    }
    &:hover + img.cover {
      display: none;
    }
  }
  img.cover {
    border: 3px solid #fff;
    height: 513px;
    width: 342px;
  }
}
</style>