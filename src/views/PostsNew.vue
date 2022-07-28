<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newUserParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts">
    <form v-on:submit.prevent="createPost()">
      <h1>New Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newUserParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newUserParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newUserParams.image" />
      </div>
      <!-- <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
      </div> -->
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
