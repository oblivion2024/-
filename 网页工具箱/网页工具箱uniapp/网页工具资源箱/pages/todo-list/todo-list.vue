<template>
  <view class="container">
    <view class="card">
      <view class="card-header">
        <text class="card-title">待办事项列表</text>
      </view>
      <view class="card-content">
        <view class="input-group">
          <input
            type="text"
            placeholder="添加新的待办事项"
            v-model="newTodo"
            class="input"
          />
          <button @click="addTodo" class="button">
            <text>添加</text>
          </button>
        </view>
        <view class="todo-list">
          <view v-for="todo in todos" :key="todo.id" class="todo-item">
            <label class="checkbox">
              <checkbox :checked="todo.completed" @change="toggleTodo(todo.id)" />
              <text :class="{ 'completed': todo.completed }">{{ todo.text }}</text>
            </label>
            <view class="todo-meta">
              <text class="todo-date">{{ todo.createdAt }}</text>
              <button @click="removeTodo(todo.id)" class="delete-button">删除</button>
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: ''
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        const now = new Date()
        const formattedDate = `${now.getMonth() + 1}/${now.getDate()}`
        this.todos.push({ 
          id: Date.now(), 
          text: this.newTodo, 
          completed: false,
          createdAt: formattedDate
        })
        this.newTodo = ''
        this.saveTodos()
      }
    },
    toggleTodo(id) {
      const todo = this.todos.find(t => t.id === id)
      if (todo) {
        todo.completed = !todo.completed
        this.saveTodos()
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      this.saveTodos()
    },
    saveTodos() {
      uni.setStorageSync('todos', JSON.stringify(this.todos))
    },
    loadTodos() {
      const storedTodos = uni.getStorageSync('todos')
      if (storedTodos) {
        this.todos = JSON.parse(storedTodos)
      }
    }
  },
  onLoad() {
    this.loadTodos()
  }
}
</script>

<style>
.input-group {
  display: flex;
  margin-bottom: 20rpx;
}
.input-group .input {
  flex: 1;
  margin-right: 16rpx;
  margin-bottom: 0;
}
.todo-list {
  margin-top: 20rpx;
}
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16rpx 0;
  border-bottom: 2rpx solid #e5e5e5;
}
.checkbox {
  display: flex;
  align-items: center;
}
.checkbox text {
  margin-left: 12rpx;
}
.completed {
  text-decoration: line-through;
  color: #888;
}
.todo-meta {
  display: flex;
  align-items: center;
}
.todo-date {
  font-size: 24rpx;
  color: #888;
  margin-right: 16rpx;
}
.delete-button {
  font-size: 24rpx;
  color: #dc3545;
  background: none;
  border: none;
  padding: 0;
}
</style>