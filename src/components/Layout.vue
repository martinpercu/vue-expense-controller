<script setup>
import { ref } from 'vue'
const showHistory = ref(false)
</script>

<template>
    <div class="header">
        <slot name="header"></slot>
    </div>
    <div class="resume">
        <slot name="resume"></slot>
    </div>
    <div class="history">
      <div class="head" @click="showHistory = !showHistory">
        <div class="grip"></div>
      </div>
      <div class="body" v-show="showHistory">
        <slot name="history"></slot>
      </div>
    </div>
</template>

<style scoped>
.header, .resume, .history {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 14px 0;
  box-sizing: border-box;
}

.header {
  position: fixed;
  width: 100vw;
}
.resume {
  min-height: 100vh;
}

.history {
  z-index: 1;
  position: absolute;
  flex-direction: column;
  bottom: 0;
  left: 1vw;
  width: 98vw;
  background-color: #f8f8f8;
  box-shadow: 0 -8px 16px #c4c4c4;
  border-radius: 20px 20px 0 0;
}

.history .head {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 24px;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}

.history .body {
  height: 75vh;
  width: 100%;
}

.history .head .grip {
  width: 120px;
  height: 8px;
  background-color: #e5e5e5;
  border-radius: 4px;
}

</style>