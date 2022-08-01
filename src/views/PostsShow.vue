<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id + ".json").then((response) => {
      this.post = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>

<template>
  <div class="posts-show">
    <div class="container">
      <h1>TESTING</h1>
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <router-link to="/posts">Back To All Posts</router-link>
      <!-- |
      <router-link v-bind:to="`/posts/${post.id}/edit`">Edit this Post</router-link> -->
    </div>
  </div>
</template>

<style></style>
