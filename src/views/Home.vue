<script>import axios from "axios";

  export default {
    data: function () {
      return {
        message: "",
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
    <div class="hero">
    <h1>Welcome to the movie app!</h1>
    </div>
    <div class="movie-list">
    <h3>Check out the movie recomendations </h3>
<div v-for=" movie in movies" v-bind:key="movie.id">
<ul>
<li> {{movie.title}}<br>
<button v-on:click="showMovie(movie)">More Info</button></li></ul>
</div>

<dialog id="movieDetails">
  <form method="dialog" class="popup">
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
<div class="add-movie">
<h2>Add a Movie:</h2>
<form>
<input type="text" v-model="createParams.title" placeholder="title"><br>
<input type="text" v-model="createParams.year" placeholder="year"><br>
<input type="text" v-model="createParams.plot" placeholder="plot"><br>
<input type="text" v-model="createParams.director" placeholder="director"><br>
<input type="text" v-model="createParams.english" placeholder="english"><br>
<input type="text" v-model="createParams.runtime" placeholder="runtime"><br>
<button v-on:click="createMovies()">Add Movie</button>
</form>
</div>
  </div>
</template>

<style>
.popup {
  width: 15em;
  margin: 0 auto;
}
.hero {
  background-image: url("https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/best-movies-1614634680.jpg");
  background-size: cover;
    height: 375px;
    padding-top: 1px;
}
.hero h1 {
  margin-top: 150px;
  color: rgb(100, 100, 101);
    font-size: 3.3em;
    text-transform: capitalize;
    background-color: rgba(255, 255, 255, 0.78);;
}
h3 {
  text-transform: capitalize;
}
ul {
  padding-inline-start: 1px;
  margin-bottom: 60px;
}
ul li {
  list-style-type: none;
  text-align: center;
  width: 33%;
    float: left;
    text-transform: capitalize;
    padding-top: 10px;
}
.movie-list {
  margin-bottom: 30px;;
}
.add-movie {
  width: 100%;
  clear: left;
  padding-top: 20px;
  background-color: #efefef6e;
}
</style>