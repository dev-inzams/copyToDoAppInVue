<script setup>
import { RouterView } from 'vue-router'
import TodoHeader from './components/TodoHeader.vue';
</script>

<template>
  <TodoHeader />

  <RouterView />
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,200;0,300;0,400;1,200;1,300;1,400&display=swap');
  *{
    font-family: "Poppins",sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .container{
    max-width: 80%;
    margin: 0 auto;
  }
</style>
