<template>
  <button @click="showTimer = !showTimer">Show/Hide</button>
  <Timer v-if="showTimer"></Timer>
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
          v-for="todo in sortedTodos"
          :key="todo.date"
          :class="{completed: todo.completed}">
        <Checkbox :label="todo.title" @check="console.log('KACHOW')" @uncheck="console.log('FINITO')"/>
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideEnded">
      Hide completed tasks
    </label>
    <p v-if="todoCounter > 0">Remaining : {{todoCounter}} task{{todoCounter > 1 ? 's' : ""}}</p>
    <Checkbox label="test"></Checkbox>
  </div>
</template>

<script setup>
import {ref, computed, onMounted} from 'vue';
import Checkbox from "./Checkbox.vue";
import Button from "./Button.vue";
import Layout from "@/Layout.vue";
import Timer from "./Timer.vue";

const newTodo = ref('')
const hideEnded = ref(false)
const todos = ref([])
const showTimer = ref(true)

onMounted(() => {
  fetch("https://jsonplaceholder.typicode.com/todos")
      .then(r => r.json())
      .then(v => todos.value = v.map(todo => ({...todo, date: todo.id})))
})

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now()
  })
  newTodo.value = ''
}

const sortedTodos = computed(() => {
  const sortedTodos = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
  if (hideEnded.value === true) {
    return sortedTodos.filter(t => t.completed === false)
  }
  return sortedTodos
})

const todoCounter = computed(() => {
  return todos.value.filter(t => t.completed === false).length
})
</script>

<style>
.completed {
  opacity: 50%;
  text-decoration: line-through;
}
</style>