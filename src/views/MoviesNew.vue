<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        newParams: {plot: ""},
        errors: []
      };
    },
    created: function() {
      
    },
    
    methods: {
      createMovie: function() {
        axios.post("/movies", this.newParams).then((response)=> {
          console.log("success", response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
      }
    },
  };
</script>

<template>
<div class="flex-box">
<div class="movie-image"> 
  <img src="https://m.media-amazon.com/images/M/MV5BNzU4NWEwNDItMzMzYy00ZDYyLWIxZjMtMDlkYWVjNjQwYzBjXkEyXkFqcGdeQXVyMDM2NDM2MQ@@._V1_FMjpg_UX1000_.jpg">
</div>
<div class="movies-new">
  <h3>Add a New Movie</h3>
<form v-on:submit.prevent="createMovie()"> <input type="text" placeholder="Title" v-model="newParams.title"><br>
<textarea type="text" placeholder="Plot" v-model="newParams.plot"></textarea><br>
<small>You have{{200 - newParams.plot.length}} charaters left.</small><br>
 <input type="text" placeholder="Year" v-model="newParams.year"><br>
 <input type="text" placeholder="Director" v-model="newParams.director"><br>
 <input type="text" placeholder="English" v-model="newParams.english"><br>
 <input type="text" placeholder="Runtime" v-model="newParams.runtime"><br>
<input type="submit" value="submit" class="submit">


</form>
  
</div>
</div>

</template>
<style>
textarea{
  width: 145px;
}
small {
  margin-top: -10px;
  font-size: 10px;
}
.flex-box {
  display: flex;
  justify-content: space-around;

}
.movie-image {
  flex-shrink: 3;
  justify-content: space-around;
  
}
.movie-image img {
  max-width: 400px;
  width: 95%;
}
.movies-new {
  flex-basis: auto;
  justify-content: start;
}

</style>