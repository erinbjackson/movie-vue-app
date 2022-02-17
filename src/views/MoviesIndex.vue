<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        movies: [],
        errors: [],
        titleFilter: ""
      };
    },
    computed: {
      filteredMovies() {
        return this.movies.filter((movie) => {
          return movie.title.toLowerCase().includes(this.titleFilter.toLowerCase());
        });
      }
    },
    created: function() {
      this.moviesIndex();
    },
    
    methods: {
      moviesIndex:function() {
        axios.get("/movies").then((response) => {
        console.log("Success", response.data);
         this.movies = response.data;
      })
      }
    },
  }
</script>

<template>
<div class="movies-index">
Search by title: <input type="text" v-model="titleFilter" list="titles">
<datalist id="titles">
  <option v-for="movie in movies" v-bind:key="movie.id">{{movie.title}}</option>
</datalist>

<transition-group appear enter-active-class="animate__animated animate__fadeInLeft" leave-active-class="animate__animated animate__fadeOutRight">
<div v-for="movie in filteredMovies" v-bind:key="movie.id">
<router-link v-bind:to="`/movies/${movie.id}`"><h3 >{{movie.title}}</h3>
 </router-link>
 </div>
 </transition-group>
</div>


</template>