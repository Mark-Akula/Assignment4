<template>
  <h1>FreeMovies4U</h1>

  <div class="movie-container">
    <label id="select" for="Movies">Choose a Movie:</label>
    <select v-model="movie">
      <option value="361743">Top Gun: Maverick</option>
      <option value="140607">Star Wars: The Force Awakens</option>
      <option value="763285">Ambulance</option>
      <option value="353081">Mission: Impossible - Fallout</option>
      <option value="634649">Spider-Man: No Way Home</option>
      <option value="505642">Black Panther: Wakanda Forever</option>
      <option value="507086">Jurassic World Dominion</option>
      <option value="384018">Fast & Furious Presents: Hobbs & Shaw</option>
      <option value="338953">Fantastic Beasts: The Secrets of Dumbledore</option>
      <option value="791373">Zack Snyder's Justice League</option>
    </select>
    <button id="getButton" @click=getSelectedOption()>Get</button>
  </div>

  <body>
    <div>
        <tr>
          <td id="left">
            <img :src="poster">
          </td>
          <td id="right">
            <p id="Title"></p>
            <p id="originalTitle"></p>
            <p id="genre" v-for="genre in genres">Genre: {{ genre.name }}</p>
            <p id="releaseDate"></p>
            <p id="Popularity"></p>
            <p id="Revenue"></p>
            <p id="voteAverage"></p>
            <p id="VoteCount"></p>
            <p id="Runtime"></p>
            <p id="synopsisHeading">Overview:</p>
            <p id="synopsisDescription">{{ overviewText }}</p>
            <iframe :src="movieTrailer"></iframe>
          </td>
        </tr>
    </div>
  </body>
</template>

<script setup>
import axios from "axios";
import { ref } from 'vue';

const movie = ref(361743);
let poster = ref("");
let title = ref("");
let originalTitle = ref("");
let genres = ref([]);
let releaseDate = ref("");
let popularity = ref("");
let revenue = ref("");
let voteAverage = ref("");
let voteCount = ref("");
let runtime = ref("");
let synopsisDescription = ref("");
let movieTrailer = ref("");

function getSelectedOption() {
  axios.get(`https://api.themoviedb.org/3/movie/${movie.value}`, {
    params: {
      api_key: "e5a15bfef5377c118448ec56598ced79",
      append_to_response: "videos",
    }
  }).then((movieData) => {
    poster.value = "https://image.tmdb.org/t/p/w500" + movieData.data.poster_path;
    title.value = movieData.data.title;
    originalTitle.value = movieData.data.original_title;
    genres.value = movieData.data.genres;
    releaseDate.value = movieData.data.release_date;
    popularity.value = movieData.data.popularity;
    revenue.value = formatPrice(movieData.data.revenue);
    voteAverage.value = movieData.data.vote_average;
    voteCount.value = movieData.data.vote_count;
    runtime.value = movieData.data.runtime;
    synopsisDescription.value = movieData.data.overview;
    movieTrailer.value = "https://www.youtube.com/embed/" + (movieData.data.videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key;
  });
}
</script>


<style scoped>
html {
  background-color: rgb(223, 207, 190);
  height: auto;
  width: auto;
}

h1 {
  text-align: center;
  color: rgb(195, 68, 122);
  text-transform: uppercase;
  font-size: 45px;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-weight: bolder;
}

select {
  color: rgb(195, 68, 122);
  padding-left: 15px;
  font-weight: bold;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size: 27px;
}

button {
  border-width: 3px;
  color: black;
  padding: 10px 10px;
  background-color: rgb(195, 68, 122);
  text-transform: uppercase;
  display: inline-block;
  font-size: 16px;
  font-weight: bolder;
  margin: 2px 2px;
  cursor: pointer;
}

#Movies {
  color: rgb(195, 68, 122);
  background-color: rgba(54, 52, 52, 0.938);
  border-color: rgba(71, 70, 70, 0.959);
  font-weight: 900;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-size: 25px;
}

#movieInfo {
  color: rgb(195, 68, 122);
  font-weight: bolder;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 18px;
  margin-left: 1%;
  left: 25px;
  text-align: left;
}

#synopsisHeading {
  padding-left: 9px;
  color: rgb(195, 68, 122);
  font-weight: bold;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 20px;
}

#synopsisDescription {
  margin-left: 10px;
  color: rgb(195, 68, 122);
  width: 660px;
  font-weight: bold;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 16px;
  text-align: left;
}

#movieTrailer {
  height: 370px;
  margin-left: 10px;
  aspect-ratio: 16 / 9;
  border-width: 5px;
  border-color: black;
  border-radius: 1%;
}

#poster {
  width: 500px;
  height: 740px;
}
</style>