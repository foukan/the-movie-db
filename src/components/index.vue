<template>
  <div class="wrapp">
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
.wrapp{
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  padding: 1.5rem;
}
.movie-card {
  font-family: 'Karla', sans-serif;
  padding: 0 .5rem;
  margin-top: 1rem;
  max-width: 255px;
  max-height: 350px;  
}
.img-area {
  position: relative;
  max-width: 100%;
  max-height: 100%;
  border-radius: 7px;
  transition: all 1.2s ease-in-out;
}
.img-area img {
  max-width: 100%;
  height: 350px;
  border-radius: 7px;
  box-shadow: 5px 9px 10px 1px #161515;
  transition: all 1.2s ease-in-out;
  opacity: .6;
}
.img-area img:hover {
  transform: scale(1.05);
  opacity: 1;
  box-shadow: 6px 12px 13px 3px #131212;
  cursor: pointer;
}
.vote {
  width: 26px;
  height: 26px;
  border-radius:100%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 10px;
  left: 5px;
  color: antiquewhite;
  font-size: .7rem;
  background-color: #c70505;
  transition: all .8s ease-in-out;
}
.img-area:hover .vote {
  opacity: .5;
  transform: scale(1.2);
}
</style>
