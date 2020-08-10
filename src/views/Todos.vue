<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo 
      @add-todo="AddTodo"
    />
    <select v-model="filter">
        <option value="all">Все</option>
        <option value="completed">Выполненные</option>
        <option value="not-completed">Активные</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <TodoList
        v-else-if="todos.length"
        v-bind:todos="todos"
        v-on:remove-todo="removeTodoItem"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader"
export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos/?_limit=3")
        .then((response) => response.json())
        .then((json) => {
            setTimeout(() => {
                this.todos = json
                this.loading = false
            }, 1000)
        });
  },
  watch: {
    filter(value) {
        loading()
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  methods: {
    removeTodoItem(id) {
      this.todos = this.todos.filter((t) => t.id !== id);
    },
    AddTodo(todo) {
      this.todos.push(todo);
    },
  },
};
</script>
