<template>
  <div class="home">

    <div v-for="post in posts">
      <h2>Posts</h2>
      <h3>Title: {{post.title}}</h3>
      <img src="post.image" alt="">
      <p>Message: {{post.body}}</p>

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
