<template>
  <div>
    <h1>Recipe info</h1>
    <h2>Title: {{ recipe.title }}</h2>
    <img v-bind:src="recipe.image_url" alt="">
    <p>Ingredients: {{ recipe.ingredients }}</p>
    <p>Directions: {{ recipe.Directions }}</p>
    <a v-bind:href="`/recipes/${recipe.id}/edit`">Edit recipe</a>
    <br>
    <a href="/recipes">Back to all recipes</a>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      recipe: {},
    };
  },
  created: function() {
    this.showRecipe();
  },
  methods: {
    showRecipe: function() {
      axios.get("/api/recipes/" + this.$route.params.id).then(response => {
        console.log("Get one recipes: ", response);
        this.recipe = response.data;
      });
    },
  },
};
</script>