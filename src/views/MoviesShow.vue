<script>
  import axios from "axios";

   export default {
    data: function () {
      return {
        movie: {},
        errors: []
      };
    },
    created: function() {
       axios.get(`http://127.0.0.1:3000/movies/${this.$route.params.id}`).then((response)=> {
          console.log("success", response.data);
          this.movie = response.data;
        });
    },
    
    methods: {
      destroyMovie: function() {
       
          axios.delete(`http://127.0.0.1:3000/movies/${this.movie.id}`).then((response) => {
            console.log("success", response.data);
            this.$router.push("/movies");
          });
        
      }
    }
     };
</script>

<template>
  <div class="movies-show">
    <h2>{{movie.title}}</h2>
    {{movie.plot}} <br>
    {{movie.year}} <br>
    {{movie.director}} <br>
    {{movie.runtime}} minutes <br>
    <button> <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit</router-link> </button> 
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>