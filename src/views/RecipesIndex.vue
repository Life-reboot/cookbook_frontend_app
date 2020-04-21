<template>
  <div class="recipes-index">
    <h1>All recipes</h1>
    Search:
    <input type="text" v-model="filterText" list="titles" />
    <datalist id="titles">
      <option v-for="recipe in recipes">{{ recipe.title }}</option>
    </datalist>
    <div v-for="recipe in filterBy(recipes, filterText, 'title', 'chef')">
      <h2>{{ recipe.title }}</h2>
      <p>Created at {{ relativeDate(recipe.created_at) }}</p>
      <p>Chef: {{ recipe.chef }}</p>
      <img v-bind:src="recipe.image_url" alt />
      <div>
        <a v-bind:href="`/recipes/${recipe.id}`">More info</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      recipes: [],
      filterText: "",
    };
  },
  created: function() {
    this.indexRecipes();
  },
  methods: {
    indexRecipes: function() {
      axios.get("/api/recipes").then(response => {
        console.log("Get all recipes: ", response);
        this.recipes = response.data;
      });
    },
    relativeDate: function(date) {
      return moment(date).fromNow();
    },
  },
};
</script>
