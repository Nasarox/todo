<template>
  <h1>To Do List</h1>
  <p v-if="tasks.length < 1">Vous n'avez rien à faire</p>
  <form action="" @submit.prevent="addTask">
    <input type="text" placeholder="Nouvelle tâche" v-model="inputTask">
    <button>Ajouter</button>
  </form>
  <hr>
  <ul>
    <li v-for="task in tasks" :key="task.date">
      {{ task.title }} - [{{new Date(task.date).toLocaleDateString()}}]
      <input type="checkbox" @click="deleteTask(task)" v-model="task.completed" />
    </li>
  </ul>
  <hr>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([
  {
    title: 'Tâche à faire',
    completed: false,
    date: Date.now(),
  },
])
const inputTask = ref('');

const addTask = () => {
  const newTask = {
    title: inputTask.value,
    completed: false,
    date: Date.now(),
  }
  tasks.value.push(newTask);
  inputTask.value = '';
}

const deleteTask = (task) => {
  tasks.value = tasks.value.filter(m => m !== task);
  task.completed = true;
}
</script>

<style>

</style>