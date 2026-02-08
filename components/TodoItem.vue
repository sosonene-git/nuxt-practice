<script setup lang="ts">
import type { Todo } from '../types/todo'

defineProps<{
  todo: Todo
}>()

const emit = defineEmits<{
  (e: 'remove', id: number): void
}>()
</script>

<template>
  <li :class="{ completed: todo.completed }">
    <label class="todo-item">
      <input type="checkbox" v-model="todo.completed" />
      <span class="text">{{ todo.text }}</span>
    </label>
    <button @click="emit('remove', todo.id)" class="delete-button" title="削除">
      ×
    </button>
  </li>
</template>

<style scoped>
li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 0;
  border-bottom: 1px solid #f9f9f9;
  transition: transform 0.2s;
}

.todo-item {
  display: flex;
  align-items: center;
  gap: 12px;
  cursor: pointer;
  flex: 1;
}

.todo-item input[type="checkbox"] {
  width: 20px;
  height: 20px;
  accent-color: #00dc82;
  cursor: pointer;
}

.text {
  font-size: 1.05rem;
  color: #2d3436;
  transition: color 0.3s, text-decoration 0.3s;
}

.completed .text {
  color: #b2bec3;
  text-decoration: line-through;
}

.delete-button {
  background: none;
  border: none;
  color: #ff7675;
  font-size: 1.5rem;
  cursor: pointer;
  padding: 0 8px;
  line-height: 1;
  transition: transform 0.2s, color 0.2s;
}

.delete-button:hover {
  transform: scale(1.2);
  color: #d63031;
}
</style>
