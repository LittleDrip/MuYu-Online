<style setup>
.article {
  position: absolute;
  bottom: 10px;
  right: 5px;
}
.dialog{
  font-family:'MiSans';
}
dialog {
  width: 400px;
  height: 400px;
  /* text-align: center; */
  line-height: 40px;
  position: absolute;
  text-align: justify;
  top: 50%;
  left: 50%;
  right: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 0.1em 0.2em rgba(0, 0, 0, 0.5), 0 0 0 50vmax rgba(0, 0, 0, 0.3);
  z-index: 99;
}

.card {
  max-width: 320px;
  border-width: 1px;
  border-color: rgba(219, 234, 254, 1);
  border-radius: 1rem;
  background-color: rgba(255, 255, 255, 1);
  padding: 1rem;
}

.header {
  display: flex;
  align-items: center;
  grid-gap: 1rem;
  gap: 1rem;
}

.icon {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 9999px;
  background-color: rgba(96, 165, 250, 1);
  padding: 0.5rem;
  color: rgba(255, 255, 255, 1);
}

.icon svg {
  height: 1rem;
  width: 1rem;
}

.alert {
  font-weight: 600;
  color: rgba(107, 114, 128, 1);
}

.message {
  margin-top: 1rem;
  color: rgba(107, 114, 128, 1);
}

.button {
  margin-left: 90px;
  position: relative;
  width: 6em;
  height: 4em;
  border: none;
  background: none;
}

.X {
  content: '';
  position: absolute;
  top: 50%;
  left: 33%;
  width: 2em;
  height: 1.5px;
  background-color: #424141;
  transform: rotate(45deg);
}

.Y {
  content: '';
  position: absolute;
  top: 50%;
  left: 33%;
  width: 2em;
  height: 1.5px;
  background-color: #383838;
  transform: rotate(-45deg);
}

.close {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  bottom: -40%;
  left: 70%;
  width: 3em;
  height: 1.7em;
  font-size: 16px;
  background-color: rgb(47, 47, 46);
  color: #000;
  border: 1px solid #000;
  pointer-events: none;
  opacity: 0;
}

.button:hover {
  background-color: rgb(210, 0, 0);
}

.button:active {
  background-color: rgb(130, 0, 0);
}

.button:hover>.close {
  animation: close 0.2s forwards 1.25s;
}

@keyframes close {
  100% {
    opacity: 1;
  }
}
</style>

<template>
    <article ref="article" class="article">
      <img @click="handleBtnClick" src="@/assets/svg/About.svg" alt="说明" />
    </article>
    <dialog ref="dialog" class="dialog">
      <div class="header">
        <p class="alert">欢迎来到Drip's MuYu</p>
        <button class="button" @click="handleDialogClick">
          <span class="X"></span>
          <span class="Y"></span>
          <div class="close">Close</div>
        </button>
      </div>
      <p class="message">
      <p style="color: gray;">&nbsp;等级制度如下：</p>
      【积德萌新】 &nbsp;&nbsp; 0功德 <br />
      【积德能手】 &nbsp; &nbsp;500功德<br />
      【积德大师】 &nbsp;&nbsp;1000功德<br />
      【在下积德僧】5000功德<br />
      【积德掌门人】20000功德<br />
      【怪盗积德】&nbsp;&nbsp; 30000功德
      </p>

    </dialog>

</template>

<script setup>
import { ref } from "vue";

const dialog = ref(null);

const handleBtnClick = () => {
  dialog.value.show();
};

const handleDialogClick = () => {
  dialog.value.close();
};
</script>
