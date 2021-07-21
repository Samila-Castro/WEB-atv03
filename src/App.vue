

<template>
  <div id="app">
    <Posts/>
    <Albums/> 
    <Todos/>

  </div>
</template>

<script>
  import Albums from './components/Albums.vue'
  import Posts from './components/Posts.vue'
  import Todos from './components/Todos.vue'


export default {
  name: 'App',
  components: {
     Posts,
     Albums,
    Todos,
   
  }
}
</script>

<style>
#app {
  font-family: sans-serif;
  text-align:justify;
  margin-top: 30px;
}
</style>
