<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input v-model="newTodo" type="text" placeholder="Task To Do"/>
      <button :disabled="newTodo.length === 0">Add</button>
    </fieldset>
  </form>
  <div v-if="todos.length === 0">No waiting task</div>
  <div v-else>
    <ul>
      <li
          v-for="(todo, index) in todos"
          :key="todo.date"
          :class="{completed: todo.completed}">
        <label>
          <input type="checkbox" v-model="todo.completed"/>
          {{ todo.title }}
        </label>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('')
const todos = ref([
    {
  title: 'Learn Vue.js',
  completed: true,
  date: Date.now()
  },
  {
    title: 'Learn JavaScript',
    completed: false,
    date: Date.now()
  }])

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })
  newTodo.value = ''
}
</script>

<style>
.completed {
  opacity: 50%;
  text-decoration: line-through;
}
</style>