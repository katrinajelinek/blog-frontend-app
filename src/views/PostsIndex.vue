<template>
  <div class="home">

     <h2>Posts</h2>
    <div v-for="post in posts">
      <h3>Title: {{post.title}}</h3>
      <p>Message: {{post.body}}</p>
      <img src="post.image" alt=""> <br>
      <router-link :to="`/posts/${post.id}`">More Info</router-link>
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
