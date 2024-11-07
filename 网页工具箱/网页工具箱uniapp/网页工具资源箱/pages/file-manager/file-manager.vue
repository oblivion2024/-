<template>
  <view class="container">
    <view class="card">
      <view class="card-header">
        <text class="card-title">数据库管理器</text>
      </view>
      <view class="card-content">
        <view class="input-group">
          <input
            type="text"
            placeholder="姓名"
            v-model="newName"
            class="input"
          />
          <input
            type="text"
            placeholder="邮箱"
            v-model="newEmail"
            class="input"
          />
          <button @click="addRecord" class="button">
            <text>添加记录</text>
          </button>
        </view>
        <view class="record-list">
          <view v-for="record in records" :key="record.id" class="record-item">
            <view class="record-info">
              <text class="record-name">{{ record.name }}</text>
              <text class="record-email">{{ record.email }}</text>
              <text class="record-date">{{ record.createdAt }}</text>
            </view>
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
.input-group {
  display: flex;
  flex-wrap: wrap;
  margin-bottom: 20rpx;
}
.input-group .input {
  flex: 1 0 45%;
  margin-right: 16rpx;
  margin-bottom: 16rpx;
}
.input-group .button {
  flex: 1 0 100%;
}
.record-list {
  margin-top: 20rpx;
}
.record-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16rpx 0;
  border-bottom: 2rpx solid #e5e5e5;
}
.record-info {
  flex: 1;
}
.record-name {
  font-size: 28rpx;
  font-weight: bold;
  margin-bottom: 4rpx;
}
.record-email {
  font-size: 24rpx;
  color: #007bff;
  margin-bottom: 4rpx;
}
.record-date {
  font-size: 24rpx;
  color: #888;
}
.delete-button {
  font-size: 24rpx;
  color: #dc3545;
  background: none;
  border: none;
  padding: 0;
}
</style>