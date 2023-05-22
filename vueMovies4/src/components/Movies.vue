<script setup>
import axios from "axios";
import { ref } from "vue";

const movie = ref(null);
const movieData = ref(false);

const getMovie = async () => {
  movieData.value = (
    await axios.get(`https:api.themoviedb.org/3/movie/${movie.value}}`, {
      params: {
        api_key: "fbb6ba03bbd1aaeb92c52f989ea8698d",
        append_to_response: "videos",
      },
    })
  ).data;

  computed: {
    getTrailerKey() => {
      const trailer = this.movieData.videos.results.find((trailer) => trailer.type === 'Trailer');
      return trailer ? trailer.key : '';
    },
  },
  };
</script>

<template>
  <header class="movie-container">
    <select v-model="movie">
      <option value="385687">Fast X</option>
      <option value="804150">Cocaine Bear</option>
      <option value="980078">Winnie the Pooh: Blood and Honey</option>
      <option value="389">12 Angry Men</option>
      <option value="13">Forrest Gump</option>
      <option value="505642">Black Panther: Wakanda Forever</option>
      <option value="315162">Puss in Boots: The Last Wish</option>
      <option value="296271">The Devil Conspiracy</option>
      <option value="502356">The Super Mario Bros. Movie</option>
      <option value="76600">Avatar: The Way of Water</option>
    </select>
    <button @click="getMovie">Get</button>
  </header>

  <div class="movieTile">
    <div v-if="movieData" class="moviePoster">
      <img :src="`https://image.tmdb.org/t/p/w500${movieData.poster_path}`" />
    </div>
  </div>

  <div v-if="movieData" class="movieTrailer">
    <iframe v-if="trailer" :src="`https://www.youtube.com/embed/${movieData.videos.results.filter((trailer) => trailer.type === 'Trailer')[0]
    .key}`"></iframe>
  </div>

  <div v-if="movieData">
    <h1>Movie Title: {{ movieData.title }}</h1>
    <h3>Release Date: {{ movieData.release_date }}</h3>
    <h4>{{ movieData.overview }}</h4>
    <h4>{{ movieData.revenue }}</h4>
    <h4>{{ movieData.runtime }}</h4>
    <h4>{{ movieData.vote_average }}</h4>
    <h4>{{ movieData.vote_count }}</h4>
    <h4>{{ movieData.popularity }}</h4>
  </div>
</template>

<style scoped>
/* * {
  box-sizing: border-box;
  padding: 0;
} */
.movie-container {
  vertical-align: top;
}
</style>
