<template>
    <h1>FreeMovies4U</h1>

  <div class="movie-container">
    <label id="select" for="Movies">Choose a Movie:</label>
    <select v-model="movie" name="Movies" id="Movies">
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

  <MovieProfile v-if="selectedMovie" :movie="selectedMovie"></MovieProfile>
</template>

<script>
import MovieProfile from './MovieProfile.vue';
import axios from "axios";
import { ref } from "vue";

export default {
  name: "MoviePage",
  components: {
    MovieProfile
  },
  data() {
    return {
      movie: ref("361743"),
      selectedMovie: null
    }
  },
  methods: {
    getSelectedOption() {
      axios.get(`https://api.themoviedb.org/3/movie/${this.movie}`, {
        params: {
          api_key: "e5a15bfef5377c118448ec56598ced79",
          append_to_response: "videos",
        }
      }).then((movieData) => {
        this.handleData(movieData);
        console.log(this.selectedMovie);
      }); 
    },
    handleData(movieData) {
      this.selectedMovie = {
        poster: "https://image.tmdb.org/t/p/w500" + movieData.data.poster_path,
        title: movieData.data.title,
        originalTitle: movieData.data.original_title,
        genres: movieData.data.genres,
        releaseDate: movieData.data.release_date,
        popularity: movieData.data.popularity,
        revenue: movieData.data.revenue,
        voteAverage: movieData.data.vote_average,
        voteCount: movieData.data.vote_count,
        runtime: movieData.data.runtime,
        synopsisDescription: movieData.data.overview,
        movieTrailer: "https://www.youtube.com/embed/" + (movieData.data.videos.results.filter((trailer) => trailer.type === "Trailer")).at(0).key,
      }
    }
  }
}
</script>

<style scoped>
h1 {
  text-align: center;
  color: rgb(195, 68, 122);
  text-transform: uppercase;
  font-size: 45px;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-weight: bolder;
}

#select {
  color: rgb(195, 68, 122);
  padding-left: 15px;
  font-weight: bold;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-size: 27px;
}

#getButton {
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
</style>