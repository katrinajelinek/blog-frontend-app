<template>
  <div class="home">
    <div>Search by title:
      <input type="text" v-model="titleFilter" placeholder="Search by title">
      <button v-on:click="setSortAttribute('id')">Sort by ID</button>
    </div>

    <h1>Posts</h1> <br>
    <div class="card-columns">
      <div class="card" v-for="post in orderBy(posts, 'title')">
        <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" class="card-img-top" alt="">
        </router-link>
        <div class="card-body">
          <h5 class="card-title">{{post.title}}</h5>
          <p class="card-text">{{post.body}}</p>
          <p class="card-text"><small class="text-muted">Created {{relativeTime(post.created_at)}}</small></p>
        </div>
      </div>
    </div>

  </div>
  
</template>

<style>
</style>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],

  data: function() {
    return {
      posts: [],
      titleFilter: "",
      sortAttribute: "title",
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
    },
    relativeTime: function (date) {
      return moment(date).fromNow();
    },
    setSortAttribute: function (attribute) {
      this.sortAttribute = attribute;
    }
  }
};
</script>
