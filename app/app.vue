<script setup>
const newTodo = ref('')
const todos = ref([
  { id: 1, text: 'Nuxtのセットアップ', completed: true },
  { id: 2, text: 'Todoリストを作る', completed: false }
])

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false
    })
    newTodo.value = ''
  }
}

const removeTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

const remainingCount = computed(() => {
  return todos.value.filter(t => !t.completed).length
})
</script>

<template>
  <div class="container">
    <div class="todo-card">
      <h1>Task Master</h1>
      
      <form @submit.prevent="addTodo" class="input-group">
        <input 
          v-model="newTodo" 
          placeholder="何をする？" 
          class="todo-input"
        />
        <button type="submit" class="add-button" :disabled="!newTodo.trim()">
          追加
        </button>
      </form>

      <div class="stats">
        <span>あと {{ remainingCount }} つのタスク</span>
      </div>

      <ul class="todo-list">
        <li v-for="todo in todos" :key="todo.id" :class="{ completed: todo.completed }">
          <label class="todo-item">
            <input type="checkbox" v-model="todo.completed" />
            <span class="text">{{ todo.text }}</span>
          </label>
          <button @click="removeTodo(todo.id)" class="delete-button" title="削除">
            ×
          </button>
        </li>
      </ul>

      <div v-if="todos.length === 0" class="empty-state">
        タスクはありません。リラックスしましょう！
      </div>
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

.stats {
  font-size: 0.9rem;
  color: #636e72;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #f0f0f0;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list li {
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

.empty-state {
  text-align: center;
  color: #b2bec3;
  padding: 2rem 0;
}
</style>
