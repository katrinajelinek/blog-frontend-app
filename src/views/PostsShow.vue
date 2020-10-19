<template>
  <div class="posts-show">

      <h3>Title: {{post.title}}</h3>
      <p>Message: {{post.body}}</p>
      <img src="post.image" alt=""> <br>

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