<template>
  <div class="home">
    <h1>New recipe</h1>
    <div>
      Title:
      <input type="text" v-model="newRecipeTitle" />
      Chef:
      <input type="text" v-model="newRecipeChef" />
      Prep time:
      <input type="text" v-model="newRecipePrepTime" />
      Ingredients:
      <input type="text" v-model="newRecipeIngredients" />
      Directions:
      <input type="text" v-model="newRecipeDirections" />
      Image url:
      <input type="text" v-model="newRecipeImageUrl" />
      <button v-on:click="createRecipe()">Create</button>
    </div>

    <h1>All recipes</h1>
    <div v-for="recipe in recipes">
      <h2>Title: {{ recipe.title }}</h2>
      <button v-on:click="currentRecipe = recipe">Show more info</button>
      <div v-if="recipe === currentRecipe">
        <p>Image: {{ recipe.image_url }}</p>
        <img v-bind:src="recipe.image_url" alt="" />
        <p>Ingredients: {{ recipe.ingredients }}</p>
        <p>Directions: {{ recipe.directions }}</p>
      </div>
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
      currentRecipe: {},
      newRecipeTitle: "",
      newRecipeChef: "",
      newRecipePrepTime: "",
      newRecipeIngredients: "",
      newRecipeDirections: "",
      newRecipeImageUrl: "",
    };
  },
  created: function() {
    axios.get("/api/recipes").then(response => {
      this.recipes = response.data;
      console.log("The recipes: ", this.recipes);
    });
  },
  methods: {
    createRecipe: function() {
      var params = {
        input_title: this.newRecipeTitle,
        input_chef: this.newRecipeChef,
        input_prep_time: this.newRecipePrepTime,
        input_ingredients: this.newRecipeIngredients,
        input_directions: this.newRecipeDirections,
        input_image_url: this.newRecipeImageUrl,
      };

      axios.post("/api/recipes", params).then(response => {
        console.log("Success!!!", response.data);
        this.recipes.push(response.data);
      });
    },
  },
};
</script>
