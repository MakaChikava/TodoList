<template>
<div>

  <h1>To Do's</h1>
  <input type="text" v-model="todoList.todo">
  <img src="https://www.freepnglogos.com/uploads/plus-icon/add-plus-icon-28.png" alt="plusLogo" id="btns" @click=" createTodo() ">
  

  <!-- List of Todos -->

<div v-for="todo in allTodos" :key="todo._id">

  <table class="table">
    <tbody>
      <tr>
        <th scope="row" v-if="todo.check" @click="todo.check = !todo.check">
          {{ todo.todo }}
        </th>
        <th scope="row" class="change" v-else @click="todo.check = !todo.check">
          {{ todo.todo }}
        </th>
        <td><img src="https://cdn4.iconfinder.com/data/icons/ionicons/512/icon-close-512.png" alt="deletebtn" id="btns" @click="deleteTodo(todo._id)"></td>
      </tr>
    </tbody>

  </table>
  <!-- <p v-if="todo.check" @click="todo.check = !todo.check">
  {{ todo.todo }}
  </p>
  

  <p class="change" v-else @click="todo.check = !todo.check">
    {{ todo.todo }} 
  </p><button @click="deleteTodo(todo._id)">delete</button> -->
  
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
#btns{
  height: 30px;
  width: 30px;
  
}
#btns:hover{
  border:5px #11d335;
}
</style>
