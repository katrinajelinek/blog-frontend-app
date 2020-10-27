<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Posts</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/posts">Posts</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/posts/1/edit">Edit</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/posts/new">New Post</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/signup">Signup</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="!isLoggedIn()" to="/login">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="isLoggedIn()" to="/logout">Logout</router-link>
          </li>
        </ul>
      </div>
    </nav>
    <div v-if="flashMessage" class="alert alert-success fade show"       role="alert">
      {{flashMessage}}
      <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
    <div class='container'>
      <router-view/>
    </div>
  </div>
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
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>

export default {
  data: function() {
    return {
      flashMessage: ""
    };
  },

  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  }
};
</script>