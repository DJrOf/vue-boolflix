<template>
  <header>
    <input type="text" v-model="search" > <button @click="cercaFilmserie" >Cerca</button>
    <section>
<div v-for="movie in movies" :key="movie.id" >
{{ movie.title }}
</div>
  </section>
  </header>
  
</template>

<script>
import axios from 'axios';

export default {
name: 'Header', 

data() {
  return {
    movies: [],
    series: [],
    search: "",
  };
},

methods: {
  fetchMovieseries() {
    axios.get(`https://api.themoviedb.org/3/search/movie?query=${ this.search }&api_key=101a61aa934c613d880b033e114051e0`, `https://api.themoviedb.org/3/search/tv?query=${ this.search }&api_key=101a61aa934c613d880b033e114051e0`)
    .then((res ) => {
      this.movies = res.data.results;

    })
  },
  cercaFilmserie() {
  this.fetchMovieseries();
  },
},
}
</script>

<style>

</style>