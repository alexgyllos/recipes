<template lang="html">
  <div v-on:click="handleClick" class="item">
    <div class="inside">
      <img :src="recipe.thumbnail" alt="">
        <div class="textitem">
          <p v-on:click="handleClick">{{recipe.title}}</p>
        </div>
    </div>
  </div>

</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'recipe-item',
  props: ['recipe'],
  methods: {
    handleClick() {
      eventBus.$emit('recipe-selected', this.recipe)
    }
  }
}
</script>

<style lang="css" scoped>
  .item {
    width: 200px;
    height: 200px;
    display: flex;
    flex-direction: column;
    /* justify-content: center; */
    align-items: center;
    text-align: center;
    margin: 3px;
    border: 1px solid black;
    border-radius: 2%;
    user-select: none;
    background: rgba(241, 250, 238, 0.7);
  }

  .item:hover {
    background: rgba(241, 250, 238, 1.0);
    cursor: pointer;
  }

  .textitem {
    /* width: 100px; */
    user-select: none;
  }

  .inside {
    width: 150px;
    height: 150px;
    margin-top: 40px;
    margin-bottom: 25px;
    /* border: 1px solid black; */
  }

  img {
    /* width: 50px; */
    border-radius: 50%;
    /* border: 0.5px solid black; */
  }
</style>
