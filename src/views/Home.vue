<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>

import Todos from '../components/Todos.vue'
import AddTodo from '../components/AddTodo.vue'

import axios from 'axios'

const URL = 'https://jsonplaceholder.typicode.com/todos/'

export default {
  name: 'app',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(deleteId) {
      axios.delete(`${URL}${deleteId}`)
        .then(res => this.todos = this.todos.filter(({id}) => id !== deleteId))
        .then(err => console.error(err))
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post(URL, {
        title, completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .then(err => console.error(err))
    }
  },
  created() {
    axios.get(`${URL}?_limit=5`)
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))
  }
}
</script>
