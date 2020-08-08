<template>
  <div id="app">
    <h1>Todo application</h1>
    <AddTodo 
      @add-todo="AddTodo"
    />
    <hr>
    <TodoList 
      v-bind:todos="todos"
      v-on:remove-todo="removeTodoItem"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'App',
    data() {
      return {
        todos: []
      }
    },
    mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos/?_limit=3')
        .then(response => response.json())
        .then(json => this.todos = json)
    },
  components: {
    TodoList, AddTodo
  },
  methods: {
    removeTodoItem(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    AddTodo(todo) {
      this.todos.push(todo)
    } 
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
