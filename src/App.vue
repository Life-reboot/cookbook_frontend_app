<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <a class="navbar-brand" href="#">Cookr</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="/">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/recipes">All recipes</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/recipes/new">New recipe</router-link>
          </li>
          <li v-if="!jwt" class="nav-item">
            <router-link class="nav-link" to="/signup">Signup</router-link>
          </li>
          <li v-if="!jwt" class="nav-item">
            <router-link class="nav-link" to="/login">Login</router-link>
          </li>
          <li v-if="jwt" class="nav-item">
            <router-link class="nav-link" to="/logout">Logout</router-link>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>

    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<style>
body {
  font-family: Futura, "Trebuchet MS", Arial, sans-serif;
  background-image: url("./assets/triangle-mosaic.png");
}
</style>

<script>
export default {
  data: function() {
    return {
      jwt: null,
      userId: null,
    };
  },
  created: function() {
    this.setJwt();
    this.setUserId();
  },
  methods: {
    setJwt: function() {
      this.jwt = localStorage.jwt;
    },
    setUserId: function() {
      this.userId = parseInt(localStorage.user_id);
    },
  },
};
</script>