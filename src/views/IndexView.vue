<script lang="ts" setup>
import Tips from "@/components/Tips.vue";
import woodenfishSound from "@/assets/sound/sound.mp3";
import card from "@/components/card.vue";
import level from "@/components/Level.vue";
import { useCounterStore } from "@/stores/counter";
import { ref } from "vue";
const counterStore = useCounterStore();
const audio = new Audio(woodenfishSound);
const volume = ref(1); // 初始化音量为 50%
const showMsg = ref(false);
const handleClick = () => {
  if (counterStore.count <= 999999) {
    counterStore.increment();
    audio.currentTime = 0;
    audio.volume = volume.value; // 设置音量
    audio.play();
    showMsg.value = true;
    setTimeout(() => {
      showMsg.value = false;
    }, 200); // 0.5 秒后隐藏消息
  }
};
let timer: any = null;
let intervalId: any;
window.addEventListener("keydown", (event) => {
  if (event.code === "Space") {
    if (timer !== null) {
      clearTimeout(timer);
    }
    // 检查是否按下了空格键
    timer = setTimeout(() => {
      handleClick();
    }, 150);
  }
});
const targetString = "drip";

const targetString2 = "zero";
const targetString3 = "subt";

let inputBuffer = "";
window.addEventListener("keydown", (event) => {
  inputBuffer += event.key.toLowerCase();

  // Keep the buffer length equal to or less than the target string length
  if (inputBuffer.length > targetString.length) {
    inputBuffer = inputBuffer.slice(-targetString.length);
  }

  if (inputBuffer === targetString) {
    counterStore.count += 5000;
    // 在这里执行你的操作
    inputBuffer = ""; // 重置缓冲区
  }
  if (inputBuffer === targetString2) {
    counterStore.count = 0;

    inputBuffer = ""; // 重置缓冲区
  }
  if (inputBuffer === targetString3) {
    counterStore.count -= 5;

    inputBuffer = ""; // 重置缓冲区
  }
});
let isRunning = ref(false);
const handleAuto = () => {
  if (isRunning.value == false) {
    isRunning.value = true;
    intervalId = setInterval(() => {
      handleClick();
    }, 500); // 每秒钟执行一次
  } else {
    clearInterval(intervalId);
    intervalId = null;
    isRunning.value = false;
  }
};
const jumpToGithub = () => {
  window.open("https://github.com/LittleDrip/MuYu-Online", "_blank");
};
// -------------------------

// -------------------------
</script>

<template>
  <div class="container">
    <Tips />
    <img class="github-svg" src="@/assets/svg/Github.svg" @click="jumpToGithub()" alt="木鱼" />
    <div class="app" style="text-align: center">
      <div class="title" style="text-align: center; margin-top: 100px">
        <card />
        <level />

        <div style="font-size: 100px" class="numberOrletter">
          {{ counterStore.count }}
        </div>

        <h1 class="h1foot" style="font-size: 20px; color: grey">功德</h1>
      </div>
      <div class="main" style="margin-top: 80px">
        <img class="icon-svg" src="@/assets/svg/Muyu.svg" @click="handleClick()" alt="木鱼" />
      </div>
      <transition name="fade" mode="out-in">
        <div v-if="showMsg" class="msg">功德+1</div>
      </transition>
      <div style="margin-top: 40px; color: gray">
        按
        <span>空格</span>
        或
        <span>敲击木鱼</span>
        即可积德
      </div>
      <div class="handle">
        <button @click="handleAuto()" :class="{ active: isRunning }">自动积德</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
span {
  background: #747272;
  border-radius: 5px;
  padding: 0 4px;
  margin: 0 1px;
  color: beige;
}
/* -------------------------- */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s ease; /* 这里将 transition 应用于所有属性 */
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-20px); /* 往上移动 20 像素 */
}
/* ------------------------------ */
.github-svg {
  position: absolute;
  size: 50px;
  top: 10px;
  right: 20px;
}
.msg {
  position: absolute; /* 使用绝对定位 */
  top: 270px; /* 调整消息位置 */
  right: 550px; /* 调整消息位置 */
  /* background-color: rgba(255, 255, 0, 0.8); 设置消息背景颜色 */
  padding: 5px 10px; /* 设置消息内边距 */
  border-radius: 5px; /* 设置消息圆角 */
}
.numberOrletter {
  font-family: "ErrorSans";
}
.app {
  font-family: "MiSans";
}
.h1foot {
  font-family: "KaiTi";
}
.handle {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 20px;
}

button {
  appearance: none;
  background-color: transparent;
  border: 0.125em solid #1a1a1a;
  border-radius: 0.9375em;
  box-sizing: border-box;
  color: #3b3b3b;
  cursor: pointer;
  display: inline-block;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif,
    "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  min-height: 3.75em;
  min-width: 0;
  outline: none;
  padding: 1em 2.3em;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(0.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  will-change: transform;
}

button:disabled {
  pointer-events: none;
}

button:hover {
  color: #fff;
  background-color: #1a1a1a;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

button:active {
  box-shadow: none;
  transform: translateY(0);
}
button.active {
  background-color: #1a1a1a;
  color: #fff;
}
</style>
