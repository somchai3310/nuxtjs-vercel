<script setup>
const route = useRoute()
const todoId = route.params.id

const BASE_URL = "https://664432576c6a656587097505.mockapi.io/"
const {data: todo} = await useFetch(`${BASE_URL}/todos/${todoId}`)


</script>
<template>
  <div>
    <pre>
      id: {{ todo.id }}
      name: {{ todo.name }}
      status: {{ todo.status }}
    </pre>
  </div>
</template>
