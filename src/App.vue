<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
    },
  },
};
</script>

<template>
  <nav class="navbar navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="#">
        <img
          src="https://images.creativemarket.com/0.1.0/ps/7414066/1820/1214/m1/fpnw/wm1/logo-design-for-movie-production-company-01-.jpg?1575502358&s=c37b3e6a8863b415070b669f6c8a457c"
          alt=""
          width="60"
          height="44"
        />
      </a>
      <nav class="nav">
        <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
        <router-link class="nav-link active" aria-current="page" to="/movies">Movies</router-link>

        <router-link v-if="isLoggedIn" class="nav-link" to="/logout">Logout</router-link>

        <router-link v-if="isLoggedIn" class="nav-link" to="/movies/new">New</router-link>
        <router-link v-if="!isLoggedIn" class="nav-link" to="/login">Login</router-link>
        <router-link v-if="!isLoggedIn" class="nav-link" to="/signup">Signup</router-link>
      </nav>
    </div>
  </nav>

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
button,
input.submit {
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
  color: #1b9480;
}
a:visited {
  color: #0a3f36;
}
</style>
