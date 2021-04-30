<template>
  <div class="movie-detail">
    <h2>
      {{ movie.Title }}
    </h2>
    <p>
      {{ movie.Year }}
    </p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-image" />
    <p>
      {{ movie.Plot }}
    </p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(async () => {
      const res = await fetch(
        `https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      );
      const data = await res.json();
      movie.value = data;
    });

    return {
      movie,
    };
  },
};
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 700;
    margin-bottom: 16px;
  }

  .featured-image {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>