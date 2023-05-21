<script setup>
import {ref} from "vue";
import axios from "axios";

const movie = ref("");

const getMovie = async () => {
  const data = (await axios.get(`https://api.themoviedb.org/3/movie/${movie.value}?api_key=${import.meta.env.VITE_TMDB_API_KEY}&language=en-US&adult=false&append_to_response=videos`)).data;
</script>

<template>
  <header>
    <select v-model="movie">
      <option value="1033219">Attack on Titans</option>
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
</template>

<style scoped>
</style>
