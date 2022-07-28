<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Check out these posts!",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts.json").then((response) => {
        this.posts = response.data;
      });
    },
  },
};
</script>

<template>
  <div v-for="post in posts" v-bind:key="post.user_id">
    <h1>{{ post.title }}</h1>
    <h2>{{ post.body }}</h2>
    <img :src="post.image" alt="POSTS" />
  </div>
</template>

<style></style>
