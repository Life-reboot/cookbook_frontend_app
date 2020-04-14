<template>
  <div class="signup">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>Edit Recipe</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>title:</label>
          <input type="text" class="form-control" v-model="recipe.title" />
        </div>
        <div class="form-group">
          <label>chef:</label>
          <input type="text" class="form-control" v-model="recipe.chef" />
        </div>
        <div class="form-group">
          <label>prepTime:</label>
          <input type="text" class="form-control" v-model="recipe.prep_time" />
        </div>
        <div class="form-group">
          <label>ingredients:</label>
          <input type="text" class="form-control" v-model="recipe.ingredients" />
        </div>
        <div class="form-group">
          <label>imageUrl:</label>
          <input type="text" class="form-control" v-model="recipe.image_url" />
        </div>
        <div class="form-group">
          <label>directions:</label>
          <input type="text" class="form-control" v-model="recipe.directions" />
        </div>
        <input type="submit" class="btn btn-primary" value="Submit" />
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      recipe: {},
      errors: [],
    };
  },
  created: function() {
    axios.get("/api/recipes/" + this.$route.params.id).then(response => {
      this.recipe = response.data;
    });
  },
  methods: {
    submit: function() {
      var params = {
        input_title: this.recipe.title,
        input_chef: this.recipe.chef,
        input_prep_time: this.recipe.prep_time,
        input_ingredients: this.recipe.ingredients,
        input_directions: this.recipe.directions,
        input_image_url: this.recipe.image_url,
      };
      axios
        .patch("/api/recipes/" + this.$route.params.id, params)
        .then(response => {
          this.$router.push("/recipes");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>