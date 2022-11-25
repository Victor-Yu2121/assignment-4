<template>
  <div class ="color">
  <h1>VMDB</h1>
  <form action="">
    <label for="movies">Search for a movie:</label>
    <select v-model = "selected">
      <option value="634649">Spider-Man: No Way Home</option>
      <option value="324857">Spider-Man: Into the Spider-Verse</option>
      <option value="429617">Spider-Man: Far from Home</option>
      <option value="347201">Boruto: Naruto the Movie</option>
      <option value="317442">The Last: Naruto the Movie</option>
      <option value="553610">Mobile Suit Gundam Narrative</option>
      <option value="284053">Thor: Ragnarok</option>
      <option value="361743">Top Gun: Maverick</option>
      <option value="438148">Minions: The Rise of Gru</option>
      <option value="810693">Jujustsu Kaisen 0</option>
    </select>
  </form>

  <button @click="getinformation">GET</button>

  <div v-if="information" class="info-container">
    <p>{{ information.title }}</p> 
    <p>Release Date: {{information.release_date}}</p>
    <p>Popularity: {{information.popularity}} </p>
    <p>Runtime: {{information.runtime}}</p>
    <p>Vote Average: {{information.vote_average}}</p>
    <p>Vote Count: {{information.vote_count}}</p>
    <p>Revenue: {{information.revenue}}</p>
    <p>Overview:</p>
    <p> {{ information.overview }}</p>
    <img :src= "`https://image.tmdb.org/t/p/w500${information.poster_path}`" alt="">
    <iframe :src= "`https://www.youtube.com/embed/${information.videos.results.filter((trailer) => trailer.type === 'Trailer').at(0).key}`" frameborder="0"></iframe>
  </div>
</div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
const selected = ref(null);
const information =  ref(false);
const getinformation = async() => {
  information.value = (
      await axios.get(`https://api.themoviedb.org/3/movie/${selected.value}`, {
        params: {
          api_key: "d91b0162a80ade40030a0ecdfb78e66b",
          append_to_response: "videos",
        },
      })
    ).data
  }

</script>



<style scoped>
  *{
  margin:0;
  padding:0;
  }
  h1 {
  text-align: center;
  color: rgb(38, 206, 198);
  font-weight: bold;
  font-size: 65px;
  font-family: 'Impact';
  }
  .info-container {
    background-color: #000000;
  }
  .color{
    background-color: #000000;
  }
  button {
  font-size: 20px;
  color: rgb(38, 206, 198);
  background-color: rgb(54, 52, 52);
  border-color: rgba(33, 255, 4, 0.76);
}
  form {
  color: rgb(38, 206, 198);
  font-family: 'Impact';
  font-size: 20px;
  }
  img{
  height: 400px;
  aspect-ratio: 9/ 9;
  border-width: 5px;
  border-color: rgba(38, 206, 198);
  }
  p{
  text-align: center;
  padding-left: 20px;
  color: rgb(38, 206, 198);
  font-weight: bold;
  font-family: Verdana, Tahoma, sans-serif;
  }
  iframe {
  height: 400px;
  aspect-ratio: 16 / 9;
}
select{
  color: rgb(38, 206, 198);
  font-family: 'Impact';
  font-size: 20px;
  background-color: #000000;
}
</style>
