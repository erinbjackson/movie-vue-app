<script>
  import axios from "axios";

  export default {
    data: function () {
      return {
        newParams: {},
        errors: []
      };
    },
    created: function() {
      
    },
    
    methods: {
      createMovie: function() {
        axios.post("http://127.0.0.1:3000/movies", this.newParams).then((response)=> {
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
<div class="movies-new">
  <h3>Add a New Movie</h3>
<form v-on:submit.prevent="createMovie()">
<label for="">Title</label> <input type="text" v-model="newParams.title"><br>
<label for="">Plot</label> <input type="text" v-model="newParams.plot"><br>
<label for="">Year</label> <input type="text" v-model="newParams.year"><br>
<label for="">Director</label> <input type="text" v-model="newParams.director"><br>
<label for="">English</label> <input type="text" v-model="newParams.english"><br>
<label for="">Runtime</label> <input type="text" v-model="newParams.runtime"><br>
<input type="submit" value="submit">


</form>
  
</div>

</template>