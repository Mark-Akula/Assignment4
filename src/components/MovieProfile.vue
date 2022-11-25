<template>
  <div>
    <table>
      <tr>
        <td id="left">
          <img :src="this.movie.poster">
        </td>
        <td id="right">
          <div id="movieInfo">
            <p id="Title">Title: {{this.movie.title}}</p>
            <p id="originalTitle">Original title: {{this.movie.originalTitle}}</p>
            <p id="genre" v-for="genre in this.movie.genres">Genre: {{ genre.name }}</p>
            <p id="releaseDate">Release Date: {{this.movie.releaseDate}}</p>
            <p id="Popularity">Popularity: {{this.movie.popularity}}</p>
            <p id="Revenue">Revenue: {{this.movie.revenue}}</p>
            <p id="voteAverage">Vote Average: {{this.movie.voteAverage}}</p>
            <p id="VoteCount">Vote Count: {{this.movie.voteCount}}</p>
            <p id="Runtime">Runtime: {{this.movie.runtime}}</p>
          </div>
          <p id="synopsisHeading">Overview:</p>
          <p id="synopsisDescription">{{ this.movie.synopsisDescription }}</p>
          <iframe id="movieTrailer" :src="this.movie.movieTrailer"></iframe>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  name: "MovieProfile",
  props: {
    movie: {
      type: Object,
      required: true
    }
  }
}
</script>


<style scoped>
#right {
  float: left;
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

#movieInfo > p {
  margin: 0;
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