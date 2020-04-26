<template lang="html">
    <div class="container">
      <h1>RECIPES</h1>
      <div class="recipes">
        <recipe-list :recipes="recipes"></recipe-list>
      </div>
      <div class="details">
        <div class="detailsbackground">
        <div class="imgdetails">
          <img v-if="selectedRecipe" :src="selectedRecipe.thumbnail" alt="">
        </div>
        <div>
          <recipe-detail v-if="selectedRecipe" :recipe="selectedRecipe" class="textdetails"></recipe-detail>
        </div>
      </div>
        <div class="">
          <button v-on:click="saveRecipe" type="button" name="button">Add Favourite</button>
        </div>
      </div>
      <div class="favourites">
        <h1>FAVOURITES</h1>
        <div class="textfavourites">
          <p v-for="favrecipe of favouriteRecipes">{{favrecipe.title}}</p>
        </div>
      </div>
    </div>
</template>

<script>
import RecipeList from './components/RecipeList.vue'
import {eventBus} from './main.js'
import RecipeDetails from './components/RecipeDetails.vue'

export default {
  name: 'app',
  data() {
    return{
      recipes: [],
      selectedRecipe: null,
      favouriteRecipes: []
    }
  },
  mounted() {
    this.getRecipes()

    eventBus.$on('recipe-selected', (recipe) => {
      this.selectedRecipe = recipe;
    })

    eventBus.$on('fave-recipe', (recipe) => {
      if(!this.favouriteRecipes.includes(recipe)) {
        this.favouriteRecipes.push(recipe)
      }
    })
  },
  methods: {
    getRecipes: function() {
      fetch("http://www.recipepuppy.com/api/")
      .then(res => res.json())
      .then(recipes => this.recipes = recipes.results)
    },
    removeFavourite: function(recipe) {

    },
    saveRecipe: function() {
      if(!this.favouriteRecipes.includes(this.selectedRecipe)) {
        this.favouriteRecipes.push(this.selectedRecipe);
      }
    }
  },
  components: {
    'recipe-list': RecipeList,
    'recipe-detail': RecipeDetails
  }
}
</script>

<style lang="css" scoped>
  .container {
    display: flex;
    flex-direction: column;
    text-align: center;
    justify-content: center;
    /* border: 1px solid black; */
    width: 80%;
    margin: auto;
    /* text-decoration: underline; */
  }

  .container h1 {
    color: rgba(241, 250, 238, 1.0);
    text-shadow: 3px 2px 1px black;
    font-size: 2.8em;
    margin: 0;
    padding: 0;
  }

  .recipes {
    justify-content: center;
    /* border: 1px solid black; */

  }

  .details {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* border: 1px solid black; */
    margin: 10px;
    /* background: rgba(230, 57, 70, 0.7) */
  }

  .details p {
    color: rgba(241, 250, 238, 1.0);
    text-shadow: 3px 2px 1px black;
    font-size: 1.5em;
    margin: 0;
    padding: 0;
    user-select: none;
  }

  .detailsbackground {
    /* background: rgba(241, 250, 238, 1.0); */
    background-image: url("https://images.unsplash.com/photo-1555505019-8c3f1c4aba5f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80");
    background-size: cover;
    color: rgba(241, 250, 238, 1.0);
    border: 1px solid rgba(241, 250, 238, 1.0);
    border-radius: 30%;
    display: flex;
    flex-direction: row;
    width: 450px;
    height: 110px;
    align-items: center;
    justify-content: center;
  }

  .imgdetails img {
    border-radius: 50%;
    border: 1px solid black;
    user-select: none;
  }

  .textdetails {
    margin-left: 5px;
    /* border: 1px solid black; */
    width: 352px;
    height: 106px;
    /* text-decoration: inherit; */
    align-items: center;
    text-shadow: 1px 0px 1px black;
    user-select: none;
    /* background: rgba(241, 250, 238, 1.0) */
  }

  button {
    background-color: rgba(241, 250, 238, 0.8);
    margin: 10px;
    transition: 0.3s;
    font-size: 1.1em;
    border: 1px solid black;
    font-family: 'Lato', sans-serif;

  }

  button:hover {
    background-color: rgba(241, 250, 238, 1);
    cursor: pointer;
  }

  .favourites {
    background-image: url("https://images.unsplash.com/photo-1555505019-8c3f1c4aba5f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80");
    background-size: cover;
    margin: 50px;
    height: 500px;
    display: flex;
    /* justify-content: center; */
    flex-direction: column;
    align-items: center;
    color: rgba(241, 250, 238, 1.0);
    text-shadow: 1px 0px 1px black;
    border-radius: 3px;
    border: 1px solid rgba(241, 250, 238, 1.0);
  }

  .textfavourites {

  }

</style>

<style>
  html {
    background-image: url("https://images.unsplash.com/photo-1584949602572-4e628835156f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1650&q=80");
    background-size: cover;
    background-attachment: fixed;
    /* background-position: center; */
    width: 100vw;
    padding: 0;
    margin: 0;
    /* overflow-x: hidden; */
    /* overflow-y: hidden; */
    font-family: 'Lato', sans-serif;
  }

</style>
