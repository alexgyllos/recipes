<template lang="html">
  <div class="details">
    <p>{{recipe.title}}</p>
    <p>{{recipe.ingredients}}</p>

  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'recipe-detail',
  props: ['recipe'],
  data() {
    return {
      recipeIngredients: null
    }
  },
  methods: {
    saveRecipe() {
      eventBus.$emit('fave-recipe', this.recipe)
    }
  }
}
</script>

<style lang="css" scoped>

  .addFavourite:hover {
    cursor: pointer;
  }
</style>
