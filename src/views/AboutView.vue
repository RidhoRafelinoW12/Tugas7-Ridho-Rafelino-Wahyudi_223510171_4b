<template>
  <div class="todo-container">
    <h1 class="title">To-Do List</h1>
    <div class="input-container">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo" 
        placeholder="Add a new task" 
        class="todo-input"
      />
      <button @click="addTodo" class="add-button">Add Task</button>
    </div>

    <ul class="todo-list">
      <li v-for="(todo, index) in todoStore.todos" :key="index" class="todo-item">
        <span 
          :class="{ completed: todo.completed }" 
          class="todo-task"
        >
          {{ todo.task }}
        </span>
        <button @click="toggleTodo(index)" class="toggle-button">
          {{ todo.completed ? 'Undo' : 'Complete' }}
        </button>
        <button @click="removeTodo(index)" class="remove-button">Remove</button>
      </li>
    </ul>

    <p class="incomplete-count">Incomplete Tasks: {{ todoStore.incompleteCount }}</p>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useTodoStore } from '../stores/countStore'

export default {
  setup() {
    const todoStore = useTodoStore()
    const newTodo = ref('')

    const addTodo = () => {
      if (newTodo.value.trim() !== '') {
        todoStore.addTodo(newTodo.value)
        newTodo.value = ''
      }
    }

    const removeTodo = (index) => {
      todoStore.removeTodo(index)
    }

    const toggleTodo = (index) => {
      todoStore.toggleTodo(index)
    }

    return {
      newTodo,
      todoStore,
      addTodo,
      removeTodo,
      toggleTodo
    }
  }
}
</script>

<style scoped>
.todo-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  color: black;
}

.title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 24px;
  color: black;
}

.input-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.todo-input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #ddd;
  border-radius: 5px;
  margin-right: 10px;
}

.add-button {
  padding: 10px 20px;
  font-size: 16px;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.add-button:hover {
  background: #218838;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.todo-task {
  flex: 1;
  font-size: 18px;
  margin-right: 10px;
}

.completed {
  text-decoration: line-through;
  color: #888;
}

.toggle-button, .remove-button {
  padding: 5px 10px;
  font-size: 14px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.toggle-button {
  background: #007bff;
  color: white;
}

.toggle-button:hover {
  background: #0056b3;
}

.remove-button {
  background: #dc3545;
  color: white;
  margin-left: 10px;
}

.remove-button:hover {
  background: #c82333;
}

.incomplete-count {
  margin-top: 20px;
  font-size: 16px;
  color: #333;
  text-align: center;
}
</style>
