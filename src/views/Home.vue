<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="recipe in recipes">
      <h2>Title: {{ recipe.title }}</h2>
      <p>Image: {{ recipe.image_url }}</p>
      <img v-bind:src="recipe.image_url" alt="" />
      <p>Ingredients: {{ recipe.ingredients }}</p>
      <p>Directions: {{ recipe.directions }}</p>
    </div>
  </div>
</template>

<style>
img {
  width: 300px;
}
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!!!!",
      recipes: [],
    };
  },
  created: function() {
    axios.get("/api/recipes").then(response => {
      this.recipes = response.data;
      console.log("The recipes: ", this.recipes);
    });
  },
  methods: {},
};
</script>
