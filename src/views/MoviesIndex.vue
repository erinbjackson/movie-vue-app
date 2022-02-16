<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        movies: [],
        errors: []
      };
    },
    created: function() {
      this.moviesIndex();
    },
    
    methods: {
      moviesIndex:function() {
        axios.get("http://127.0.0.1:3000/movies").then((response) => {
        console.log("Success", response.data);
         this.movies = response.data;
      })
      }
      
    
    },
  };
</script>

<template>
<div class="movies-index">
<div v-for="movie in movies" v-bind:key="movie.id">
 <router-link v-bind:to="`/movies/${movie.id}`"> <h3>{{movie.title}}</h3></router-link>


</div>
</div>

</template>