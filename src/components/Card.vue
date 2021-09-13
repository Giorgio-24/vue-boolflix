<template>
  <div>
    <div
      class="card-structure position-relative m-4"
      v-for="element in list"
      :key="element.id"
    >
      <ul class="card-list position-absolute bg-dark text-white px-4">
        <li class="mb-3">
          <ul>
            <li>{{ element.genre_ids }}</li>
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
              Average: {{ getAverage(element.vote_average) }}
              <i
                :class="
                  getAverage(element.vote_average) < 1
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(element.vote_average) < 2
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(element.vote_average) < 3
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(element.vote_average) < 4
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
              <i
                :class="
                  getAverage(element.vote_average) < 5
                    ? 'far fa-star'
                    : 'fas fa-star color-gold'
                "
              ></i>
            </li>
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
  </div>
</template>

<script>
export default {
  name: "card",
  props: ["list"],
  data() {
    return {};
  },
  methods: {
    getFlag(language) {
      if (language == "en") {
        return require(`../assets/images/en.png`);
      } else if (language == "it") {
        return require(`../assets/images/it.png`);
      } else {
        return;
      }
    },
    getAverage(average) {
      return Math.ceil(average / 2);
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