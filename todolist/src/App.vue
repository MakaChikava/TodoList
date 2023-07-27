<template>
<div>

  <h1>To Do's</h1>
  <input type="text" v-model="todoList.todo">
  <button @click=" createTodo() ">submit</button>

  <h3>list of allTodos</h3>

<div v-for="todo in allTodos" :key="todo._id">
  <p v-if="todo.check" @click="todo.check = !todo.check"> 
  {{ todo.todo }} 
  </p>
  

  <p class="change" v-else @click="todo.check = !todo.check">
    {{ todo.todo }} 
  </p><button @click="deleteTodo(todo._id)">delete</button>
  
</div>

</div>
</template>

<script>

import axios from 'axios'
export default {

  name: 'App',

  data(){
    
    return{

      awesome: false,

      allTodos:[],

      todoList:{
        todo:"",
        check: true
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
    this.refreshData()
  })
},

deleteTodo(id){
axios
  .delete(`http://localhost:8000/todo/${id}`)
  .then(()=>{
    this.refreshData()
    
  })
},

// switch list item from true to false vice versa
handleToggle(){

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
.change{
  text-decoration: line-through;
}
</style>
