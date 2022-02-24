<script>
export default {
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem('jwt');
    }
  }

};
</script>

<template>
  <div id="nav">
    <router-link to="/">Home</router-link>|
    <router-link to="/movies">Movies</router-link> |
    <span v-if="isLoggedIn()">
    <router-link to="/logout">Logout</router-link> |
    <router-link  to="/movies/new">New</router-link> 
    </span>
    <span v-else>
      <router-link to="/login">Login</router-link> |
      <router-link to="/signup">Signup</router-link> |
    </span>

  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 0px;
  background-color: #333;
  color: #fff;
  margin-top: -8px;
}

#nav a {
  font-weight: bold;
  color: #fff;
  padding: 8px;
  
}

#nav a.router-link-exact-active {
  color: #42b983;
}
button, input.submit {
  color: #147060;
    background-color: #fff;
    border: 2px solid #147060;
    border-radius: 5px;
    padding: 5px 10px;
    margin: 10px 10px;
}
.main-content {
  margin-top: 50px;
}
a {
  color:#1b9480;
}
a:visited {
  color: #0a3f36
}
</style>
