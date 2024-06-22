<script lang="ts" setup>
import { useCounterStore } from "@/stores/counter";

import { onMounted, ref, watch, watchEffect } from "vue";
import anime from "@/components/anime.vue";
import notification from "@/components/notification.vue";

const counterStore = useCounterStore();
const notificationRef: any = ref(null);

const callNotify = () => {
  if (notificationRef.value) {
    notificationRef.value.showNotification();
  }
};
let level = ref("");
let levelInfo = ref("");
let plusCount = ref();
watchEffect(() => {
  if (counterStore.count < 500) {
    levelInfo.value = "积德萌新";
    level.value = "Lv1";
    plusCount.value = 500 - counterStore.count;
  } else if (counterStore.count < 1000) {
    levelInfo.value = "积德能手";
    level.value = "Lv2";
    plusCount.value = 1000 - counterStore.count;
  } else if (counterStore.count < 5000) {
    levelInfo.value = "积德大师";
    level.value = "Lv3";
    plusCount.value = 5000 - counterStore.count;
  } else if (counterStore.count < 20000) {
    levelInfo.value = "在下积德僧";
    level.value = "Lv4";
    plusCount.value = 20000 - counterStore.count;
  } else if (counterStore.count < 30000) {
    levelInfo.value = "积德掌门人";
    level.value = "Lv5";
    plusCount.value = 30000 - counterStore.count;
  } else if (counterStore.count <= 99999) {
    levelInfo.value = "怪盗积德";
    level.value = "Lv6";
    plusCount.value = counterStore.count <= 30000 ? "0" : "0"; // 使用三元运算符简化
  } else if (counterStore.count >= 100000) {
    levelInfo.value = "怪盗积德";
    level.value = "Lv6";
    plusCount.value = counterStore.count <= 30000 ? "0" : "-1"; // 使用三元运算符简化
  }

  if (counterStore.count === 100000) {
    levelInfo.value = "怪盗积德";
    level.value = "Lv6";
    plusCount.value = counterStore.count <= 30000 ? "0" : "-1"; // 使用三元运算符简化
    callNotify();
  }
});

onMounted(() => {
  // Example of accessing child component's method after parent is mounted
  if (notificationRef.value) {
    console.log("Child component is mounted");
  }
});
</script>

<template>
  <div>
    <notification ref="notificationRef" />

    <div class="card">
      <span style="background: #747272; font-size: 30px; color: #fff; border-radius: 5px">
        {{ level }}
      </span>

      <div class="card__content">
        <p class="card__title">{{ levelInfo }}</p>
        <p class="card__description" v-if="plusCount != 0 && plusCount != -1">
          距离下一级还差{{ plusCount }}功德
        </p>
        <p class="card__description" v-if="plusCount == 0"><br />&nbsp;功德圆满！</p>
        <p class="card__description" v-if="plusCount == -1">
          <anime />
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  position: absolute;
  /* top: 60px;
  right: 15px; */
  top: 90px;
  right: 380px;
  width: 150px;
  height: 120px;
  background-color: #fff;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  perspective: 1000px;
  box-shadow: 0 0 0 5px #fff;
  transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card span {
  width: 60px;
  padding: 2px 8px 2px 8px;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 8px;
}

.card__content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 20px;
  box-sizing: border-box;
  background-color: #fff;
  transform: rotateX(-90deg);
  transform-origin: bottom;
  transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card:hover .card__content {
  transform: rotateX(0deg);
}

.card__title {
  margin: 0;
  font-size: 24px;
  color: #333;
  font-weight: 700;
}

.card:hover svg {
  scale: 0;
}

.card__description {
  margin: 10px 0 0;
  font-size: 14px;
  color: #777;
  line-height: 1.4;
}
</style>
