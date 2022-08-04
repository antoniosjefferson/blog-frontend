<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function () {
    return {
      message: "Check out these posts!",
      posts: [],
      currentPost: [],
      // nameFilter: "",
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
    relativeTime: function (date) {
      return moment(date).fromNow();
    },
  },
};
</script>

<template>
  <!-- <h1>
    Search:
    <input v-model="nameFilter" type="text" />
  </h1> -->
  <div v-for="post in posts" v-bind:key="post.user_id">
    <div
      v-for="post in posts"
      v-bind:key="post.user_id"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
    ></div>
    <h1>{{ post.title }}</h1>
    <h2>{{ post.body }}</h2>
    Updated
    <p>{{ relativeTime(post.updated_at) }}</p>
    <img :src="post.image" alt="POSTS" />
  </div>
</template>

<style>
.selected {
  background-color: blueviolet;
}
</style>
