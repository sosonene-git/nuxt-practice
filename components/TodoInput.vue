<script setup lang="ts">

const newTodo = ref('')

const emit = defineEmits<{
  (e: 'add', text: string): void
}>()

const handleAdd = () => {
  if (newTodo.value.trim()) {
    emit('add', newTodo.value)
    newTodo.value = ''
  }
}
</script>

<template>
  <form @submit.prevent="handleAdd" class="input-group">
    <input 
      v-model="newTodo" 
      placeholder="何をする？" 
      class="todo-input"
    />
    <button type="submit" class="add-button" :disabled="!newTodo.trim()">
      追加
    </button>
  </form>
</template>

<style scoped>
.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 1.5rem;
}

.todo-input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 12px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

.todo-input:focus {
  outline: none;
  border-color: #00dc82;
}

.add-button {
  background: #00dc82;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 12px;
  font-weight: 700;
  cursor: pointer;
  transition: transform 0.2s, background 0.2s;
}

.add-button:hover:not(:disabled) {
  background: #00c575;
  transform: translateY(-2px);
}

.add-button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
</style>
