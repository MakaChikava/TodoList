<template>
  <h1>To Do's</h1>
  <input type="text">
  <button>submit</button>
  <allTodos/>
</template>

<script>
import allTodos from './components/allTodos.vue';

export default {
  name: 'App',
  components: {
    allTodos
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
