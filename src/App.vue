<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form @submit.prevent="addTodo" class="form-group">
      <input v-model="newTodo" required placeholder="New todo" class="todo-input">
      <button class="todo-btn">Add Todo</button>
    </form>
    <ul class="todo-list">
      <li v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <input type="checkbox" v-model="todo.done" class="todo-checkbox">
        <span :class="{ done: todo.done }" class="todo-text">{{ todo.text }}</span>
        <button @click="editTodo(todo)" class="btn edit-btn">Edit</button>
        <button @click="removeTodo(todo)" class="btn delete-btn">X</button>
      </li>
    </ul>
    <button @click="hideCompleted = !hideCompleted" class="toggle-btn">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

let id = 0;

const newTodo = ref('');
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: 'Belajar HTML', done: false },
  { id: id++, text: 'Belajar JavaScript', done: false },
  { id: id++, text: 'Belajar Vue', done: false }
]);

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value;
});

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = '';
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}

function editTodo(todo) {
  const newText = prompt('Enter new text', todo.text);
  if (newText !== null) {
    todo.text = newText;
  }
}
</script>

<style>
body {
  background: linear-gradient(to right, rgb(0, 255, 234), rgb(255, 255, 255));
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background-color: white;
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(165, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #45efff;
}

.form-group {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.todo-input {
  padding: 10px;
  border: 2px solid rgb(30, 144, 255);
  border-radius: 5px;
  flex-grow: 1;
  margin-right: 10px;
}

.todo-btn {
  padding: 10px 20px;
  border: none;
  background-color: rgb(30, 225, 255);
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

.todo-btn:hover {
  background-color: rgb(24, 205, 205);
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-checkbox {
  margin-right: 10px;
}

.todo-text {
  flex-grow: 1;
}

.todo-text.done {
  text-decoration: line-through;
  color: rgb(169, 169, 169);
}

.btn {
  padding: 5px 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.edit-btn {
  background-color: rgb(0, 238, 255);
  color: white;
  margin-right: 5px;
}

.edit-btn:hover {
  background-color: rgb(32, 218, 199);
}

.delete-btn {
  background-color: rgb(20, 220, 193);
  color: white;
}

.delete-btn:hover {
  background-color: rgb(34, 176, 178);
}

.toggle-btn {
  margin-top: 20px;
  padding: 10px;
  border: none;
  background-color: rgb(30, 251, 255);
  color: white;
  border-radius: 5px;
  cursor: pointer;
  display: block;
  width: 100%;
}

.toggle-btn:hover {
  background-color: rgb(52, 245, 255);
}
</style>
