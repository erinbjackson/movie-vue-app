<script>import axios from "axios";

  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        movies: [],
        createParams: {},
        currentMovie: {},
        updateParams: {}

      };
    },
    created: function () {
      this.indexMovies();
    },
    methods: {
      indexMovies: function() {
        axios.get("/movies").then((response) => { console.log(response.data);
        this.movies = response.data 
      });
      },
      createMovies: function() {
        axios.post("/movies", this.createParams).then((response) => { console.log("success", response.data);
        this.movies.push(response.data);
        this.createParams = {};
      })
    },
      showMovie: function(movie) {
        console.log(movie);
        this.currentMovie = movie;
        // this.updateParams = movie;
        document.querySelector("#movieDetails").showModal();
      },

     updateMovie: function (movie) {
       
       axios.patch(`/movies/${movie.id}`, movie).then((response) => {
         console.log("success!", response.data);
       })
       .catch((error) => {
         console.log(error.response.data.errors);
       })
     },
    destroyMovie: function(movie) {
      axios.delete(`/movies/${movie.id}`).then((response) => {
        console.log("success", response.data);
        var i = this.movie.indexOf(movie);
        this.movie.splice(i, 1);
      });
    }
    },
  };
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
<div v-for=" movie in movies" v-bind:key="movie.id">
<p>{{movie.id}}: {{movie.title}}</p>
<button v-on:click="showMovie(movie)">More Info</button>

<dialog id="movieDetails">
  <form method="dialog">
    <h3>Movie Info</h3>
  <p>{{currentMovie.title}}</p>
  <p>{{currentMovie.year}}</p>
  <p>{{currentMovie.plot}}</p>
  <h3>Enter Movie Updates</h3>
  
  <input type="text"  v-model="updateParams.title" placeholder="title"><br>
  <input type="text"  v-model="updateParams.year" placeholder="year"><br>
  <input type="text" placeholder="plot" v-model="updateParams.plot"><br>
  <input type="text" placeholder="director" v-model="updateParams.director"><br>
  <input type="text" placeholder="english" v-model="updateParams.english"><br>
  <input type="text" placeholder="runtime" v-model="updateParams.runtime"><br>
  <button v-on:click="updateMovie(currentMovie)">Update</button>
  <button v-on:click="destroyMovie(currentMovie)">Delete</button> <button>Close</button>
  </form>

</dialog>
</div>
<div>
<h2>Add a Movie:</h2>
<input type="text" v-model="createParams.title" placeholder="title"><br>
<input type="text" v-model="createParams.year" placeholder="year"><br>
<input type="text" v-model="createParams.plot" placeholder="plot"><br>
<input type="text" v-model="createParams.director" placeholder="director"><br>
<input type="text" v-model="createParams.english" placeholder="english"><br>
<input type="text" v-model="createParams.runtime" placeholder="runtime"><br>
<button v-on:click="createMovies()">Add Movie</button>
</div>
  </div>
</template>

<style></style>