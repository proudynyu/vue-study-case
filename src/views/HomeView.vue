<script setup>
import { ref } from 'vue'

let id = 0
const newTodo = ref('')
const todos = ref([])

function addTodo() {
  todos.value.push({
    id: id++,
    text: newTodo.value
  })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <main>
    <form @submit.prevent="addTodo" class="input-container">
      <input v-model="newTodo" placeholder="New Todo" />
      <button>Add Todo</button>
    </form>
    <ul>
        <li v-for="todo in todos" :key="todo.id">
            {{ todo.text }} <button @click="removeTodo(todo)">X</button>
        </li>
    </ul>

  </main>
</template>

<style scoped>
main {
  width: 100%;
  height: 100%;
  align-items: center;
  justify-content: center;
  display: flex;
  flex-direction: column;
}

button {
  width: 100px;
  padding: 8px 16px;
  outline: none;
  background: green;
  color: white;
  font-weight: bold;
  border: 0;
  border-radius: 8px;
  transition: 0.2s ease-in-out;
  cursor: pointer;
}

button:hover {
  filter: brightness(1.1);
}

form {
    display: flex;
    gap: 1rem;
}

ul {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    margin-top: 1rem;
    padding: 0.5rem;
    min-width: 300px;
}

li {
    list-style: none;
    display: flex;
    justify-content: space-between;
    width: 100%;
}

li:not(:first-child) {
    margin-top: 8px;
}

li > button {
    max-width: 60px;
}
</style>
