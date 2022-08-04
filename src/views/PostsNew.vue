<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <img v-if="status" :src="`http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
        <small></small>
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <!-- <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newPostParams.password_confirmation" />
      </div> -->
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
