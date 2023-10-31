<template>
  <h1>Приложение "Список задач" на Vue 3</h1>
  <form @submit.prevent="addNewTodo">
    <label>Новая задача</label>
    <input v-model="newTodo" name="newTodo">
    <button>Добавить задачу</button>
  </form>
  <button @click="removeAllTodos">Убрать всё</button>
  <button @click="markAllDone">Отметить все как готово</button>
  <ul>
   <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
<h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h3>
<button @click="removeTodo(index)">Убрать задачу</button>
  </li> 
  </ul>
  
</template>


<script>

import { ref } from 'vue'

export default {
setup() {
  const newTodo = ref('');
  const todos = ref([]);

  function addNewTodo() {
    todos.value.push({
      id: Date.now(),
      done: false,
      content: newTodo.value,
    });
  }

  function toggleDone(todo) {
    todo.done = !todo.done;
  }

  function removeTodo(index) {
    todos.value.splice(index, 1);
  }

  function markAllDone() {
    todos.value.forEach((todo) => todo.done = true);
  }

  function removeAllTodos() {
    todos.value = [];
  }

  return {
    todos,
    newTodo,
    addNewTodo, 
    toggleDone,
    removeTodo,
    markAllDone,
    removeAllTodos,
  }
}
}

</script>


<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
  text-align:center;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>