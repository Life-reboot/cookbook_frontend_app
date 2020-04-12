<template>
  <div class="signup">
    <div class="container">
      <form v-on:submit.prevent="submit()">
        <h1>New Recipe</h1>
        <ul>
          <li class="text-danger" v-for="error in errors">{{ error }}</li>
        </ul>
        <div class="form-group">
          <label>title:</label>
          <input type="text" class="form-control" v-model="title" />
        </div>
        <div class="form-group">
          <label>chef:</label>
          <input type="text" class="form-control" v-model="chef" />
        </div>
        <div class="form-group">
          <label>prepTime:</label>
          <input type="text" class="form-control" v-model="prepTime" />
        </div>
        <div class="form-group">
          <label>ingredients:</label>
          <input type="text" class="form-control" v-model="ingredients" />
        </div>
        <div class="form-group">
          <label>imageUrl:</label>
          <input type="text" class="form-control" v-model="imageUrl" />
        </div>
        <div class="form-group">
          <label>directions:</label>
          <input type="text" class="form-control" v-model="directions" />
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
      title: "",
      chef: "",
      prepTime: "",
      ingredients: "",
      directions: "",
      imageUrl: "",
      errors: [],
    };
  },
  methods: {
    submit: function() {
      var params = {
        input_title: this.title,
        input_chef: this.chef,
        input_prep_time: this.prepTime,
        input_ingredients: this.ingredients,
        input_directions: this.directions,
        input_image_url: this.imageUrl,
      };
      var myVariable = 0;
      axios
        .post("/api/recipes", params)
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