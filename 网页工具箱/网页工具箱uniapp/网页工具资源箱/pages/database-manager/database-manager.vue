<template>
  <view class="container">
    <view class="card">
      <view class="card-header">
        <text class="card-title">数据库管理器</text>
      </view>
      <view class="card-content">
        <view class="flex mb-4">
          <input
            type="text"
            placeholder="姓名"
            v-model="newName"
            class="input mr-2"
          />
          <input
            type="text"
            placeholder="邮箱"
            v-model="newEmail"
            class="input mr-2"
          />
          <button @click="addRecord" class="button">
            <text class="button-text">添加记录</text>
          </button>
        </view>
        <view class="record-list">
          <view v-for="record in records" :key="record.id" class="record-item">
            <text class="record-id">{{ record.id }}</text>
            <text class="record-name">{{ record.name }}</text>
            <text class="record-email">{{ record.email }}</text>
            <text class="record-date">{{ record.createdAt }}</text>
            <button @click="removeRecord(record.id)" class="delete-button">删除</button>
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
      records: [],
      newName: '',
      newEmail: ''
    }
  },
  methods: {
    addRecord() {
      if (this.newName.trim() !== '' && this.newEmail.trim() !== '') {
        const now = new Date()
        const formattedDate = `${now.getMonth() + 1}/${now.getDate()}/${now.getFullYear()}`
        this.records.push({
          id: Date.now(),
          name: this.newName,
          email: this.newEmail,
          createdAt: formattedDate
        })
        this.newName = ''
        this.newEmail = ''
        this.saveRecords()
      }
    },
    removeRecord(id) {
      this.records = this.records.filter(record => record.id !== id)
      this.saveRecords()
    },
    saveRecords() {
      uni.setStorageSync('records', JSON.stringify(this.records))
    },
    loadRecords() {
      const storedRecords = uni.getStorageSync('records')
      if (storedRecords) {
        this.records = JSON.parse(storedRecords)
      }
    }
  },
  onLoad() {
    this.loadRecords()
  }
}
</script>

<style>
.container {
  padding: 20px;
}
.card {
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
.card-header {
  padding: 16px;
  border-bottom: 1px solid #e5e5e5;
}
.card-title {
  font-size: 18px;
  font-weight: bold;
}
.card-content {
  padding: 16px;
}
.input {
  border: 1px solid #e5e5e5;
  border-radius: 4px;
  padding: 8px;
  flex: 1;
}
.button {
  background-color: #007bff;
  border-radius: 4px;
  padding: 8px 16px;
}
.button-text {
  color: #ffffff;
}
.record-list {
  margin-top: 16px;
}
.record-item {
  display: flex;
  align-items: center;
  padding: 8px 0;
  border-bottom: 1px solid #e5e5e5;
}
.record-id, .record-name, .record-email, .record-date {
  flex: 1;
}
.delete-button {
  color: #dc3545;
}
</style>