<script>
import { defineNuxtComponent } from 'nuxt/app';

export default defineNuxtComponent({
  data: () => ({
    todoList: [],
  }),
  methods: {
    fetchTodoList() {
      fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => {
        this.todoList = json;
      });
    }
  }
})
</script>

<template>
  <div>
    <img src="/todo.jpg" alt="todo">
    <h1>Hello world</h1>
    <button @click="fetchTodoList()">Fetch</button>
    <ul>
      <li v-for="todo in todoList" :key="`todo-${todo.id}`">
        <input type="checkbox" :checked="todo.completed" /> {{ todo.title }}
      </li>
    </ul>
  </div>
</template>
