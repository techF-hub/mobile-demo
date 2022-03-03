<template>
<view class="home-container">
  <view class="title">收集信息</view>
  <view class="list-wrap">
    <view class="item-wrap" v-for="(item,index) in data" :key="index">
      <text class="item-text">{{index+1}}. {{item.question}}</text>

      <radio-group class="group" v-if="item.type === 'radio'">
        <label class="group-item" v-for="(cItem,cIndex) in item.answerList" :key="cIndex">
          <radio :value="cIndex" style="transform:scale(0.7)">&emsp;{{ cItem }}</radio>
        </label>
      </radio-group>

      <checkbox-group class="group" v-else-if="item.type === 'checkbox'">
        <label class="group-item" v-for="(cItem,cIndex) in item.answerList" :key="cIndex">
          <checkbox :value="cIndex" style="transform:scale(0.7)">&emsp;{{ cItem }}</checkbox>
        </label>
      </checkbox-group>

      <view class="textarea-wrap" v-else-if="item.type === 'textarea'">
        <textarea class="textarea" placeholder="输入"></textarea>
      </view>

    </view>
  </view>
  <button class="btn">提&emsp;交</button>
</view>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'
interface dataType {
  question:string;
  answerList: any[];
  type: string;
}
const data = ref<dataType[]>([
  {
    question: '近期是否到达过深圳？',
    answerList: ['是','否'],
    type: 'radio'
  },
  {
    question: '近期是否到达过深圳？',
    answerList: ['一','二'],
    type: 'checkbox'
  },
  {
    question: '近期是否到达过深圳？',
    answerList: ['一','二'],
    type: 'textarea'
  },
])
</script>

<style lang="scss" scoped>
.home-container {
  padding: 30rpx;
  padding-bottom: $safe-env;
  padding-bottom: $safe-con;
  .title {
    font-size: 36rpx;
    text-align: center;
    margin-bottom: 30rpx;
    color: rgb(0, 128, 255);
  }
  .list-wrap {
    .item-wrap {
      .item-text {
        display: block;
        color: rgb(51, 51, 51);
        margin-bottom: 16rpx;
        margin-top: 24rpx;
      }
      
      .group {
        display: flex;
        flex-direction: column;
        border: 1px solid #e0e0e0;
        .group-item {
          font-size: 36rpx;
          padding: 20rpx 30rpx;
          border-bottom: 1px solid #e0e0e0;
          &:last-of-type {
            border-bottom: none;
          }
        }
      }

      .textarea-wrap {
        .textarea {
          width: calc(100% - 40rpx);
          height: 150rpx;
          background-color: #e0e0e0;
          padding: 20rpx;
          font-size: 28rpx;
        }
      }
    }
  }
  .btn {
    margin-top: 60rpx;
    border-radius: 4px;
    background-color: rgb(0, 128, 255);
    color: rgb(255, 255, 255);
    &::after {
      border: none;
    }
  }
}
</style>
