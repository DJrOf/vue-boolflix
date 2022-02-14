<template>
<div>
<header>
  <h1>Boolflix</h1>
  <div class="searchbar" >
  <input type="text" v-model="search"> <button @click="cercaFilmserie">Cerca</button>
  </div>
  
  </header>
  <main>
    <h2>Film</h2>
    <section>
      
      <div class="card"  v-for="movie in movies" :key="movie.id" >
        
     <ul>
       <li><strong>Title:</strong>  {{ movie.title }}</li>
       <!-- <li><img src="'https://image.tmdb.org/t/p/w500' + `{{ movie.poster_path }}`" alt=""></li> -->
       <li> <strong>Original Title:</strong>  {{ movie.original_title }}</li>
       <li> <strong>Original Language:</strong> {{ movie.original_language }}</li>
      <!-- <li>  <img :src="`@/assets/img/{{ movie.original_language }}.png`" alt=""> </li>  -->
       <li> <strong>Vote:</strong> {{ movie.vote_average }}</li>
     </ul>
     
      </div>
      </section>

  <h2>Serie tv</h2>
  <section>
      
      <div class="card" v-for="serie in series" :key="serie.id" >
        
      <ul>
       <li><strong>Title:</strong> {{ serie.title }}</li>
         <li><img :src= "`https://image.tmdb.org/t/p/w92{{movie.poster_path}}`" alt=""></li>  
       <li><strong>Original Title:</strong> {{ serie.original_title }}</li>
       <li><strong>Original Language:</strong> {{ serie.original_language }}</li>
       <li><strong>Vote:</strong> {{ serie.vote_average }}</li>
     </ul>
      </div>
  </section>
  </main>
</div>
  
  
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
      this.series = res.data.results;
    })
  },
  cercaFilmserie() {
  this.fetchMovieseries();
  },
},

}
</script>

<style>

* {
  font-family: 'Raleway', sans-serif;
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
}

header {
  padding: 20px;
  height: 35px;
  background-color: #E16F00;
  display: flex;
  justify-content: space-between;
}

body {
  background-color:  dodgerblue ;
  color: white;
}

section {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0;
  margin-bottom: 20px;
}

main {
  padding: 20px;
}

.card {
  height: 160px;
  width: calc((100vw / 12) * 2);
  border: 1px solid darkgrey;
  margin: 10px;
  padding: 1%;
}

ul {
  list-style: none;
}

/* Stronger and cooler */
strong {
  font-size: larger; 
  color: #E16F00;
} 

li {
  color: white;
}


</style>

