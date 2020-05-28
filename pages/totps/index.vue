<template>
  <main class="container mt-5">
    <div class="row">
      <div class="col-12 text-right mb-4">
        <div class="d-flex justify-content-between">
          <h3>La Recipes</h3>
          <nuxt-link to="/recipes/add" class="btn btn-info">Add Recipe</nuxt-link>
        </div>
      </div>
      <template v-for="totp in totps">
        <div :key="totp.id" class="col-lg-3 col-md-4 col-sm-6 mb-4">
          <recipe-card :onDelete="deleteRecipe" :recipe="totp"></recipe-card>
        </div>
      </template>
    </div>
  </main>
</template>

<script>
import RecipeCard from "~/components/recipecard.vue";

const sampleData = [
  {
    id: 1,
    name: "Jollof Rice",
    picture: "/images/food-1.jpeg",
    ingredients: "Beef, Tomato, Spinach",
    difficulty: "easy",
    prep_time: 15,
    prep_guide:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Omnis, porro. Dignissimos ducimus ratione totam fugit officiis blanditiis exercitationem, nisi vero architecto quibusdam impedit, earum "
  },
  {
    id: 2,
    name: "Macaroni",
    picture: "/images/food-2.jpeg",
    ingredients: "Beef, Tomato, Spinach",
    difficulty: "easy",
    prep_time: 15,
    prep_guide:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Omnis, porro. Dignissimos ducimus ratione totam fugit officiis blanditiis exercitationem, nisi vero architecto quibusdam impedit, earum "
  },
  {
    id: 3,
    name: "Fried Rice",
    picture: "/images/banner.jpg",
    ingredients: "Beef, Tomato, Spinach",
    difficulty: "easy",
    prep_time: 15,
    prep_guide:
      "Lorem ipsum dolor sit amet consectetur adipisicing elit. Omnis, porro. Dignissimos ducimus ratione totam fugit officiis blanditiis exercitationem, nisi vero architecto quibusdam impedit, earum "
  }
];

export default {
    head() {
        return {
            title: "Recipes list"
        };
    },
    components: {
        RecipeCard
    },
    async asyncData({ $axios, params }) {
      try {
        // let recipes = await sampleData;
        let totps = await $axios.$get(`/totps/`);
        return { totps };
      } catch (e) {
        console.log(e);
        return { totps: [] };
      }
    },
    data() {
        return {
            totps: []
        };
    },
    methods: {
        async deleteRecipe(recipe_id) {
          try {
            await this.$axios.$delete(`/totps/${recipe_id}/`);    
            let newRecipes = await this.$axios.$get("/totps");
            this.recipes = newRecipes;
          } catch(e) {
            console.log(e);
          }
        }
    }
};
</script>
<style scoped>
</style>