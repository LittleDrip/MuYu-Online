<script lang="ts" setup>
import { useCounterStore } from "@/stores/counter";
import { ref } from "vue";
const counterStore = useCounterStore();
let level = ref("");
let levelInfo = ref("");
if (counterStore.count > 0) {
  levelInfo.value = "积德萌新";
  level.value = "Lv1";
}
if (counterStore.count > 500) {
  levelInfo.value = "积德能手";
  level.value = "Lv2";
}
if (counterStore.count > 1000) {
  levelInfo.value = "积德大师";
  level.value = "Lv3";
}
if (counterStore.count > 5000) {
  levelInfo.value = "在下积德僧";
  level.value = "Lv4";
}
if (counterStore.count > 20000) {
  levelInfo.value = "积德掌门人";
  level.value = "Lv5";
}
if (counterStore.count > 30000) {
  levelInfo.value = "怪盗积德";
  level.value = "Lv6";
}
</script>

<template>
  <div>
    <div class="card">
      <span style="background: #808080; font-size: large">
        {{ level }}
      </span>
      <div class="card__content">
        <p class="card__title">{{ levelInfo }}</p>
        <p class="card__description">距离下一级还差{{ 10000 - counterStore.count }}功德</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  position: absolute;
  top: 60px;
  right: 15px;
  width: 150px;
  height: 100px;
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
  padding: 2px 0px 2px 0px;
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
