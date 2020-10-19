<template>
  <div class="posts-show">

      <h3>Title: {{post.title}}</h3>
      <p>Message: {{post.body}}</p>
      <img :src="post.image" alt=""> <br>
      <router-link :to="`/posts/${post.id}/edit`">Edit</router-link> |
      <router-link to="/posts">Posts</router-link>

  </div>
  
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {},
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {}
};
</script>