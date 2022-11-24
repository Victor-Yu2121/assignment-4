<script setup>
// setup lang="ts"
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from 'vue'
import axios from 'axios'
const selected = ref(null);
const movieInfo =  ref(false);
const getMovieInfo = async() => {
  movieInfo.value = (
      await axios.get(`https://api.themoviedb.org/3/movie/${selected.value}`, {
        params: {
          api_key: "d91b0162a80ade40030a0ecdfb78e66b",
          append_to_response: "videos",
        },
      })
    ).data
  }
  // const trailers = data.videos.results.filter((trailer) => trailer.type === "Trailer");
</script>

<template>
  <form action="">
    <label for="movies">Pick a movie:</label>
    <select v-model = "selected">
      <option value="634649">Spider-Man: No Way Home</option>
      <option value="324857">Spider-Man: Into the Spider-Verse</option>
      <option value="429617">Spider-Man: Far from Home</option>
      <option value="3347201">Boruto: Naruto the Movie</option>
      <option value="5317442">The Last: Naruto the Movie</option>
      <option value="553610">Mobile Suit Gundam Narrative</option>
      <option value="6284053">Thor: Ragnarok</option>
      <option value="361743">Top Gun: Maverick</option>
      <option value="438148">Minions: The Rise of Gru</option>
      <option value="810693">Jujustsu Kaisen 0</option>
    </select>
  </form>

  <button @click="getMovieInfo">GET</button>

  <!-- <div :style="{backgroundImage:`url(https://image.tmdb.org/t/p/w500${movieInfo.backdrop_path})`}"></div> -->
  <div class="info-container">
    <img :src= "`https://image.tmdb.org/t/p/w500${movieInfo.poster_path}`" alt="">
    <div class="info">
      <h1>{{ movieInfo.title }}</h1> 
      <p>Release Date: {{movieInfo.release_date}} | Popularity: {{movieInfo.popularity}} | Runtime: {{movieInfo.runtime}}</p>
      <p>Vote Average: {{movieInfo.vote_average}} | Vote Count: {{movieInfo.vote_count}}</p>
      <h2>Overview:</h2>
      <p> {{ movieInfo.overview }}</p>
      <!-- <iframe :src= "`https://www.youtube.com/embed/${trailers.at(0).key}`" frameborder="0"></iframe> -->
    </div>
  </div>
</template>

<style scoped>
  body {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    color: white;
    background-color: beige;
  }
  .info-container {
    display: flex;
    padding: 5%;
    background-color: rgba(0, 0, 0, 0.5);
  }
  .info {
    padding: 5%;
  }
  button {
    background-color: black;
    color: white;
    font-size: 18px;
    padding: 10px;
    margin: 10px;
  }
  form {
    padding: 20px;
    background-color: rgba(0, 0, 0, 0.5);
  }
</style>
