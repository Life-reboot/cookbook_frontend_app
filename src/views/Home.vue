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
      <button v-on:click="destroyRecipe(recipe)">Destroy</button>
      <button v-on:click="currentRecipe = recipe">Show more info</button>
      <div v-if="recipe === currentRecipe">
        <p>Image: {{ recipe.image_url }}</p>
        <img v-bind:src="recipe.image_url" alt />
        <p>Ingredients: {{ recipe.ingredients }}</p>
        <p>Directions: {{ recipe.directions }}</p>
        <div>
          <h4>Edit recipe</h4>Title:
          <input type="text" v-model="recipe.title" />
          Chef:
          <input type="text" v-model="recipe.chef" />
          Prep time:
          <input type="text" v-model="recipe.prep_time" />
          Ingredients:
          <input type="text" v-model="recipe.ingredients" />
          Directions:
          <input type="text" v-model="recipe.directions" />
          Image url:
          <input type="text" v-model="recipe.image_url" />
          <button v-on:click="updateRecipe(recipe)">Update</button>
        </div>
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
    updateRecipe: function(recipe) {
      var params = {
        input_title: recipe.title,
        input_chef: recipe.chef,
        input_prep_time: recipe.prep_time,
        input_ingredients: recipe.ingredients,
        input_directions: recipe.directions,
        input_image_url: recipe.image_url,
      };

      axios.patch("/api/recipes/" + recipe.id, params).then(response => {
        console.log("Success!!!", response.data);
      });
    },
    destroyRecipe: function(recipe) {
      console.log("Destroy recipe...", recipe.title);
      axios.delete("/api/recipes/" + recipe.id).then(response => {
        console.log("Success!!!");
        var index = this.recipes.indexOf(recipe);
        this.recipes.splice(index, 1);
      });
    },
  },
};
</script>
