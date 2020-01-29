<template>
  <div id="app">
    <!-- <router-link to="/home">Home</router-link>
    <router-link to="/about">About</router-link> -->
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Header from './components/layout/Header.vue'
import Todos from './components/Todos.vue'
import AddTodo from './components/AddTodo.vue'
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data: function() {
    return {
      todos: [],
    }
  },
  methods: {
    deleteTodo(id) {
      // this.todos = this.todos.filter(todo => todo.id != id);

      // delete todo with axios
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => this.todos = this.todos.filter(todo => todo.id != id))
        .catch(err => err)
    },
    addTodo(newTodo) {
      // this.todos = [...this.todos, newTodo];

      // add todo with axios
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed,
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => err)
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos/?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => err)
  }
}
</script>

<style>
#app {
  
}
</style>
