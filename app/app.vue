<script setup lang="ts">
import type { Todo } from '../types/todo'

const newTodo = ref('')
const todos = ref<Todo[]>([
  { id: 1, text: 'Nuxtのセットアップ', completed: true },
  { id: 2, text: 'Todoリストを作る', completed: false }
])

const addTodo = (text: string) => {
  todos.value.push({
    id: Date.now(),
    text,
    completed: false
  })
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo: Todo) => todo.id !== id)
}

const remainingCount = computed(() => {
  return todos.value.filter((t: Todo) => !t.completed).length
})
</script>

<template>
  <div class="container">
    <div class="todo-card">
      <h1>Task Master</h1>
      
      <TodoInput @add="addTodo" />

      <TodoStats :count="remainingCount" />

      <TodoList :todos="todos" @remove="removeTodo" />

      <EmptyState v-if="todos.length === 0" />
    </div>
  </div>
</template>

<style scoped>
.container {
  min-height: 100vh;
  background: linear-gradient(135deg, #00dc82 0%, #34cdfe 100%);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Inter', sans-serif;
  padding: 20px;
}

.todo-card {
  background: white;
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  width: 100%;
  max-width: 450px;
}

h1 {
  color: #2d3436;
  text-align: center;
  margin-bottom: 2rem;
  font-weight: 800;
  letter-spacing: -1px;
}
</style>
