<template>
  <div class="demo" @touchmove="onTouchMoveOuter">
    <div :catch-move="isLongPressed">
      <div
          v-for="(block,index) in blockList"
          :key="index"
          @longpress="onLongPress"
          @touchend="onTouchEnd"
          @touchmove="onTouchMove"
      >
        <div
            style="width: 200px;height: 100px;margin: 10px; background-color: #f4f">
          {{ block + index }}
        </div>
      </div>
    </div>

  </div>
</template>

<script setup>
import {ref} from 'vue';
import Taro from "@tarojs/taro";


// 不能根据isLongPressed动态调整catchMove
const isLongPressed = ref(false);
const blockList = ref(new Array(20).fill('block'))
const onLongPress = () => {
  isLongPressed.value = true
  Taro.vibrateShort();
  console.log('long press')
};

const onTouchEnd = () => {
  isLongPressed.value = false
  console.log('touch end')
}
const onTouchMove = () => {
  console.log('touch move ...')

}

const onTouchMoveOuter = () => {
  console.log('outer touch move ...')

}
</script>

<style>
.demo {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>