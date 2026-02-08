<script setup lang="ts">
import type { Todo } from '../types/todo'

defineProps<{
  todos: Todo[]
}>()

const emit = defineEmits<{
  (e: 'remove', id: number): void
}>()
</script>

<template>
  <ul class="todo-list">
    <TodoItem 
      v-for="todo in todos" 
      :key="todo.id" 
      :todo="todo" 
      @remove="emit('remove', $event)"
    />
  </ul>
</template>

<style scoped>
.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
