<script setup>
const BASE_URL = "https://664432576c6a656587097505.mockapi.io/"

const todos = ref([])
const todoText = ref('')

const loadTodo = async () => {
  const {data} = await useFetch(`${BASE_URL}/todos`)
  todos.value = data.value
}

const addTodo = async () => {
  try {
    await useFetch(`${BASE_URL}/todos`, {
    method: 'post',
    body: {
      name: todoText.value,
      status: 'Pending'
    }
  })
  await loadTodo()
  } catch (error) {
    console.log('error', error);
  }
  
}

const editTodo = async (todoId, todoData) => {
  try {
    await useFetch(`${BASE_URL}/todos/${todoId}`, {
    method: 'put',
    body: {
      status: todoData.status
    }
  })
  await loadTodo()
  } catch (error) {
    console.log('error', error);
  }
}

loadTodo()
</script>

<template>
  <div>
    {{ todoText }}
    <input v-model="todoText" type="text">
    <button @click="addTodo()">Add</button>
  </div>
  <ul>
    <li v-for="todo in todos">
    {{ todo?.id }}
    {{ todo?.name }}
    <!-- {{ todo?.status }} -->
    <select v-model="todo.status">
      <option>Pending</option>
      <option>Doing</option>
      <option>Done</option>
    </select>
    <button @click="editTodo(todo.id, todo)">update</button>
    <NuxtLink :to="`/todos/${todo.id}`">Edit</NuxtLink>
  </li>
  </ul>
</template>