<template>
  <ul class="cards-list">
    <li class="mb-3" v-for="element in list" :key="element.id">
      <ul>
        <li>
          Title: <span v-if="element.title">{{ element.title }}</span>
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
      </ul>
      <ul>
        <li>
          <img
            :src="`https://image.tmdb.org/t/p/w342/${element.poster_path}`"
            :alt="`${element.title}-cover`"
          />
        </li>
      </ul>
    </li>
  </ul>
</template>

<script>
export default {
  name: "card",
  props: ["list"],
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
      return Math.ceil(average % 2);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>