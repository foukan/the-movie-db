<template>
  <div>
    <div v-for="movie in movies" :key="movie.id" class="movie-card">
        <div class="img-area">
          <img :src="imgUrl + movie.poster_path" :alt="movie.original_title" />
          <p class="vote">{{movie.vote_average}}</p>
        </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "index",

  data() {
    return {
      movies: [],
    };
  },

  created() {
    axios
      .get(
        "https://api.themoviedb.org/3/list/7088229?api_key=1eb430fbd3b81b35e755cfa007a12cec&language=tr"
      )
      .then((response) => (this.movies = response.data.items))
      .catch((error) => {
        this.errors.push(error);
      });
  },

  computed: {
    imgUrl() {
      return `https://image.tmdb.org/t/p/w500/`;
    },
  },
  
};
</script>

<style scoped=true>
.movie-card {
  display: flex;
  float: left;
  font-family:  Roboto,  sans-serif;
  padding: .5rem;
  margin-bottom: 2rem;
  margin-top: 2rem;
  max-width: 300px;
  max-height: 400px;
  
}

.img-area {
  position: relative;
  max-height: 350px;
  max-width: 250px;
  border-radius: 7px;
  transition: all 1.2s ease-in-out;
}
.img-area img {
  max-width: 100%;
  border-radius: 7px;
  box-shadow: 5px 9px 10px 1px #161515;
  transition: all 1.2s ease-in-out;
  opacity: .6;
}
.img-area img:hover{
  transform: scale(1.05);
  opacity: 1;
  cursor: pointer;
}
.vote{
  color: antiquewhite;
  font-size: .7rem;
  text-align: center;
  background-color: #c70505;
  border-radius:100%;
  padding: .4em;
  position: absolute;
  top: 10px;
  left: 5px;
  transition: all 1.2s ease-in-out;
}
.img-area:hover .vote{
  opacity: .5;
  transform: scale(1.2);
}

</style>