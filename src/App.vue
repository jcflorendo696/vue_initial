<template>
  <div id="app">
    <Header />
    <AddToDo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/header';
import AddToDo from './components/AddToDo';
import axios from 'axios';


export default {
  name: 'app',
  components: {
    Todos,
    Header,
    AddToDo
  },
  data(){
    return{
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter( todo => todo.id != id );
    },
    addTodo(newTodo){
      this.todos = [...this.todos, newTodo];
    },
    created() {
      axios.get('https://jsonplaceholder.typicode.com/todos')
        .then( res => this.todos = res.data )
    }
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover{
    background: #666;
  }
</style>
