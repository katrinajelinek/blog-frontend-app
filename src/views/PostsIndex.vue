<template>
  <div class="home">
    <h1>Posts</h1> <br>
    <div class="card-columns">
      <div class="card" v-for="post in posts">
        <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" class="card-img-top" alt="">
        </router-link>
        <div class="card-body">
          <h5 class="card-title">{{post.title}}</h5>
          <p class="card-text">{{post.body}}</p>
          <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
        </div>
      </div>
    </div>

  </div>
  
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      posts: []
    };
  },
  created: function() {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/api/posts").then(response => {
        console.log(response.data);
        this.posts = response.data;
      });
    }
  }
};
</script>
