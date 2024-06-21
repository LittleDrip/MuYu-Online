<script lang="ts" setup></script>

<template>
  <div>
    <div class="card">
      <div class="img">Drip's MuYu</div>
      <div class="textBox">
        <p class="text head">敲电子木鱼</p>
        <p class="text head">积赛博功德</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  position: absolute;
  top: 15px;
  left: 15px;
  width: 250px;
  height: 80px;
  background: #fff;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: rgb(0, 0, 0);
  transition: 0.2s ease-in-out;
}

.img {
  font-family: "ErrorSans";
  height: 40%;
  top: 10px;
  left: 10px;
  font-size: 40px;
  position: absolute;
  transition: 0.2s ease-in-out;
  z-index: 1;
}

.textBox {
  opacity: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  transition: 0.2s ease-in-out;
  z-index: 2;
}

.textBox > .text {
  font-weight: bold;
}

.textBox > .head {
  font-size: 20px;
}

.textBox > .price {
  font-size: 17px;
}

.textBox > span {
  font-size: 12px;
  color: rgb(0, 0, 0);
}

.card:hover > .textBox {
  opacity: 1;
}

.card:hover > .img {
  height: 65%;
  filter: blur(7px);
  animation: anim 3s infinite;
}

@keyframes anim {
  0% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-20px);
  }

  100% {
    transform: translateY(0);
  }
}

.card:hover {
  transform: scale(1.04) rotate(-1deg);
}
</style>
