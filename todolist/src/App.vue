<template>
<div>
  <h1>To Do's</h1>
  <input type="text" v-model="todoList.todo">
  <button @click=" createTodo() ">submit</button>
  <h3>list of allTodos</h3>

<p v-for="todo in allTodos" :key="todo._id"> 
{{ todo.todo }}
</p>
</div>
</template>

<script>

import axios from 'axios'
export default {

  name: 'App',

  data(){
    
    return{

      allTodos:[],

      todoList:{
        todo:"",
        check: false
    }

  };
  },
  methods: {

    refreshData(){
axios
    .get('http://localhost:8000')
    .then((res)=>{
        console.log(res.data)
        this.allTodos = res.data
    })
},

createTodo(){
axios
  .post('http://localhost:8000/todo', {
    todo: this.todoList.todo,
    check: this.todoList.check
})
  .then((res)=>{
    console.log(res.data)
    this.refreshData
  })
},

deleteTodo(){

}


},

mounted:function()
    {
    this.refreshData();
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
