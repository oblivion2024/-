<template>
  <view class="container">
    <view class="card weather-card">
      <view class="card-header">
        <text class="card-title">天气预报</text>
      </view>
      <view class="card-content">
        <view class="flex mb-4">
          <input
            type="text"
            placeholder="输入城市名"
            v-model="city"
            class="input mr-2"
          />
          <button @click="getWeather" class="button">
            <text class="button-text">获取天气</text>
          </button>
        </view>
        <view v-if="weather" class="weather-info">
          <text class="temperature">{{ weather.temperature }}°C</text>
          <text class="condition">{{ weather.condition }}</text>
        </view>
      </view>
    </view>

    <view class="card news-card">
      <view class="card-header">
        <text class="card-title">本地新闻</text>
      </view>
      <view class="card-content">
        <view v-for="item in news" :key="item.id" class="news-item">
          <text class="news-title">{{ item.title }}</text>
          <text class="news-content">{{ item.content }}</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      weather: null,
      news: []
    }
  },
  methods: {
    getWeather() {
      // 模拟天气API调用
      this.weather = {
        temperature: Math.floor(Math.random() * 30) + 10,
        condition: ['晴朗', '多云', '雨天'][Math.floor(Math.random() * 3)]
      }
    },
    loadNews() {
      // 模拟获取新闻
      this.news = [
        { id: 1, title: "本地新闻标题1", content: "这是本地新闻1的内容..." },
        { id: 2, title: "本地新闻标题2", content: "这是本地新闻2的内容..." },
        { id: 3, title: "本地新闻标题3", content: "这是本地新闻3的内容..." },
      ]
    }
  },
  onLoad() {
    this.loadNews()
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
  margin-bottom: 20px;
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
.weather-info {
  margin-top: 16px;
  text-align: center;
}
.temperature {
  font-size: 36px;
  font-weight: bold;
}
.condition {
  font-size: 18px;
  color: #888888;
}
.news-item {
  margin-bottom: 16px;
  border-bottom: 1px solid #e5e5e5;
  padding-bottom: 16px;
}
.news-title {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 8px;
}
.news-content {
  font-size: 14px;
  color: #555555;
}
</style>