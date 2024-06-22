<script lang="ts" setup>
import { ref } from "vue";

const notificationVisible = ref(false);
const message = ref("功德圆满！彩蛋达成！");

const showNotification = () => {
  notificationVisible.value = true;
  setTimeout(() => {
    notificationVisible.value = false;
  }, 3000); // Notification will disappear after 3 seconds
};
defineExpose({
  showNotification,
});
</script>

<template>
  <div id="app">
    <div v-if="notificationVisible" class="notification">
      {{ message }}
    </div>
  </div>
</template>

<style scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  background-color: #007bff;
  border: none;
  color: white;
  border-radius: 5px;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

.notification {
  position: absolute;
  top: 5%;
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #44a15a;
  color: white;
  border-radius: 5px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  animation: fadeIn 0.5s, fadeOut 0.5s 2.5s;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
</style>
