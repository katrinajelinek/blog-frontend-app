<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="post.title" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="post.body" />
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="post.image" />
      </div>
      <input type="submit" class="btn btn-primary" value="Update" />
    </form>
    <button v-on:click="destroyPost()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      post: {},
      errors: [],
    };
  },
  created: function() {
    axios.get(`/api/posts/${this.$route.params.id}`).then(response => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    updatePost: function() {
      var params = {
        title: this.post.title,
        body: this.post.body,
        image: this.post.image,
      };
      axios
        .patch(`/api/posts/${this.post.id}`, params)
        .then((response) => {
          
          this.$router.push(`/posts/${this.post.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyPost: function () {
      if (confirm("Are you sure you want to delete this post?")) {
        axios.delete(`/api/posts/${this.post.id}`).then(response => {
          console.log("Success", response.data);
          this.$router.push("/posts");
        });
      }
    }
  },
};
</script>