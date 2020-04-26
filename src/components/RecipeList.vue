<template lang="html">
  <div class="recipes">
    <recipe-item v-for="recipe of recipes" :recipe="recipe"></recipe-item>
  </div>
</template>

<script>
import RecipeItem from './RecipeItem.vue'

export default {
  name: 'recipe-list',
  props: ['recipes'],
  components: {
    'recipe-item': RecipeItem
  }
}
</script>

<style lang="css" scoped>
  .recipes{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: baseline;
    width: 100%;
    height: 100%;
  }
</style>
