<template>
<div>
<header>
  <h1>Boolflix</h1>
  <div class="searchbar" >
  <input type="text" v-model="cerca"> <button @click="search(cerca)">Cerca</button>
  </div>
  
  </header>
  <main>
    <h2>Film</h2>

    <section>
        <div class="card"  v-for="movie in movies" :key="movie.id" >
          <img class="posterimg" :src="`https://image.tmdb.org/t/p/w342/${ movie.poster_path }`" alt="">
          <ul class="infor">
            <li><strong>Title:</strong>  {{ movie.title }}</li>
            <li><strong>Original Title:</strong>  {{ movie.original_title }}</li>
            <!-- <li><img class="flag" :src="srcFlag" alt=""> </li>   -->
            <li><strong>Vote:</strong> {{ movie.vote_average }}</li>
          </ul>
        </div>
      </section>

      <h2>Serie tv</h2>
      <section>
          
          <div class="card" v-for="serie in series" :key="serie.id" >
            <img class="posterimg" :src="`https://image.tmdb.org/t/p/w342/${ serie.poster_path }`" alt="">
          <ul>
          <li><strong>Title:</strong> {{ serie.name }}</li>
            <!-- <li><img :src= "`https://image.tmdb.org/t/p/w92 ${movie.poster_path}`" alt=""></li>   -->
          <li><strong>Original Title:</strong> {{ serie.original_name }}</li>
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
    cerca: "",
    api : {
     language: "it-IT",
     baseUri: "https://api.themoviedb.org/3",
     key: "101a61aa934c613d880b033e114051e0",
    },
  };
},

methods: {

search(cerca) {
if (!cerca) {
  this.movies = [];
  this.series = [];
  return;
}
const { key, language } = this.api;
const config = {
  params: {
    language,
    api_key: key,
    query: cerca,
  },
};

this.fetchMovieseries('search/movie', config, 'movies');
this.fetchMovieseries('search/tv', config, 'series');

},

  fetchMovieseries(endpoint, config, target) {
    axios.get(`${this.api.baseUri}/${endpoint}`, config)
    .then((res ) => {
      if (target == 'movies') {
        this.movies = res.data.results;
      } else {
        this.series = res.data.results;
      }
     
    })
    .catch((err) => {
      console.log(err);
    });
  },
},
// computed: {
//   srcFlag() {
//     return require(`@/assets/img/${ this.item.original_language }.png`);
//   }
// }
};
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
  /* height: 160px;
  width: calc((100vw / 12) * 2); */
  background-color: #E16F00;
  margin: 10px;
  padding: 0;
  width: 342px;
  height: 513px;
}

ul {
  max-width: 650px;
 list-style: none;
 position: relative;
 margin: 20px;
}


/* Stronger and cooler */
strong {
  font-size: larger; 
  color: dodgerblue;
} 

li {
  color: white;
}

.posterimg {
 position: absolute;
 z-index: 5;
 height: 513px;
 width: 342px;
}

.posterimg:hover {
  display: none;
}

.flag {
  width: 50px;
  height: 40px;
} 


</style>

