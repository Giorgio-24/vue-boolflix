<template>
  <div>
    <p v-for="(actor, index) in cast" :key="index">
      {{ actor }}
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Actors",
  props: ["id"],
  data() {
    return {
      cast: [],
    };
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/movie/${this.id}/credits?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=it-IT`
        //!https://api.themoviedb.org/3/movie/27205/credits?api_key=a49fd2ad1915c16f5b21a815b7e90362&language=en-US
      )
      .then((res) => {
        for (let i = 0; i < 5; i++) {
          this.cast.push(res.data.cast[i].name);
        }
      })
      .catch((warning) => {
        console.log(warning);
      });
  },
};
</script>

<style>
</style>