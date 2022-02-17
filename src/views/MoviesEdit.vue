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
      axios.get(`/movies/${this.$route.params.id}`).then((response)=> {
        console.log("Movie To Edit", response.data);
        this.movie = response.data;
      })
    },
    methods: {
      updateMovie: function() {
        axios.put(`/movies/${this.movie.id}`, this.movie).then((response) => {
          console.log("success", response.data);
          this.$router.push(`/movies/${this.movie.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
      }
    },
   };
   </script>
   <template>
   <div class="movies-update">
   <h2>Update A Movie</h2>
   
   <form v-on:submit.prevent="updateMovie()">
   <ul><li v-for="error in errors" v-bind:key="error"></li></ul>
   <p>Current Movie: {{movie}}</p>
<label>Title: </label><input type="text" v-model="movie.title" ><br>
<label>Plot: </label><input type="text" v-model="movie.plot" ><br>
<label>Director: </label><input type="text" v-model="movie.director" ><br>
<label>Year: </label><input type="text" v-model="movie.year" ><br>
<label>English: </label><input type="text" v-model="movie.english" ><br>
<label>Runtime: </label><input type="text" v-model="movie.runtime" ><br>
<input type="submit" value="Submit">
</form>
</div>
   </template>