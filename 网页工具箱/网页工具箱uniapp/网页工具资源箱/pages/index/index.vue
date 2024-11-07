<template>
  <view class="container">
    <text class="title">我的工具箱</text>
    <view class="grid">
      <view v-for="(item, index) in tools" :key="index" class="card-wrapper">
        <navigator :url="item.url" class="card">
          <view class="card-content">
            <text class="card-title">{{ item.title }}</text>
            <text class="card-description">{{ item.description }}</text>
          </view>
          <view class="card-button">
            <text class="button-text">进入</text>
          </view>
        </navigator>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      tools: [
        { title: '待办事项', description: '创建和管理您的待办事项列表', url: '/pages/todo-list/todo-list' },
        { title: '文件管理', description: '管理和组织您的文件', url: '/pages/file-manager/file-manager' },
        { title: '天气新闻', description: '查看天气预报和最新新闻', url: '/pages/weather-news/weather-news' },
        { title: '数据库管理', description: '管理您的数据库', url: '/pages/database-manager/database-manager' }
      ]
    }
  }
}
</script>

<style>
.container {
  padding: 20rpx;
  background-color: #f0f2f5;
  min-height: 100vh;
}
.title {
  font-size: 48rpx;
  font-weight: bold;
  text-align: center;
  margin: 40rpx 0;
  color: #333;
}
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.card-wrapper {
  width: 48%;
  margin-bottom: 20rpx;
}
.card {
  background-color: #ffffff;
  border-radius: 16rpx;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.1);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  height: 100%;
}
.card-content {
  padding: 24rpx;
  flex-grow: 1;
}
.card-title {
  font-size: 32rpx;
  font-weight: bold;
  margin-bottom: 12rpx;
  color: #333;
}
.card-description {
  font-size: 24rpx;
  color: #666;
}
.card-button {
  background-color: #007bff;
  padding: 16rpx;
  text-align: center;
}
.button-text {
  color: #ffffff;
  font-size: 28rpx;
  font-weight: bold;
}
</style>