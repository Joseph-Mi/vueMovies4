<script setup>
import axios from "axios";
import { ref } from "vue";
const TMDB_API_KEY = `fbb6ba03bbd1aaeb92c52f989ea8698d`;

const movie = ref(null);
const movieData = ref(false);

const getMovie = async () => {
  movieData.value = (
    await axios.get(
      `https:api.themoviedb.org/3/movie/${movie.value}?api_key=${TMDB_API_KEY}&language=en-US&adult=false&append_to_response=videos`
    )
  ).data;
  console.log(movieData.value);
};
// const trailers = movieData.resuls.filter((trailer) => trailer.type === `Trailer`).at(0).key;
</script>

<template>
  <h1 class="title">Movie Mania</h1>
  <div class="movie-container">
    <header>
      <div class="headBar">
        <select v-model="movie">
          <option disabled selected value="">Select Movie</option>
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
      </div>
    </header>

    <div class="movieTile">
      <div v-if="movieData" class="moviePoster">
        <img :src="`https://image.tmdb.org/t/p/w500${movieData.poster_path}`" />
      </div>

      <div class="notPoster">
        <div v-if="movieData" class="movieInfo">
          <h1>Movie Title: {{ movieData.title }}</h1>
          <h3>Release Date: {{ movieData.release_date }}</h3>
          <h4>Description: {{ movieData.overview }}</h4>
          <h4>Total Revenue: ${{ movieData.revenue }}</h4>
          <h4>Movie Length: {{ movieData.runtime }} mins</h4>
          <h4>Average Rating: {{ movieData.vote_average }}/10</h4>
          <h4>Based on {{ movieData.vote_count }} ratings</h4>
          <h4>Polularity Rating: {{ movieData.popularity }}</h4>
        </div>

        <div v-if="movieData" class="movieTrailer">
        <iframe
          :src="`https://www.youtube.com/embed/${
            movieData.videos.results
              .filter((trailer) => trailer.type === `Trailer`)
              .at(0).key
          }`"
        />
      </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0%;
  background-color: black;
}

h1 {
  font-weight: bold;
}

.title {
  display: grid;
  justify-content: center;
  font-size: 5vw;
  justify-content: center;
  background-color: rgb(89, 3, 16);
}

.movie-container {
  display: grid;
  padding: 0%;
  justify-content: center;
}

.headBar {
  display: grid;
  justify-content: center;
  padding-bottom: 20px;
  padding-top: 10px;
}

img {
  margin-top: 7%;
  height: 500px;
  aspect-ratio: 11/16;
}

.movieTile {
  display: flex;
  margin: 5%;
  justify-content: top;
  font-size: small;
}

.notPoster {
  margin-left: 50px;
  display: flex;
  flex-wrap: wrap;
}

iframe {
  margin-left: 20px;
  margin-top: 20px;
  height: 250px;
  aspect-ratio: 16/9;
}

button {
  border-radius: 5%;
  border-width: 2px;
  border-color: rgb(200, 78, 78);
}
.movieInfo {
  padding: 20px;
}
</style>
