<script setup lang="ts">
import ModelIntro from '~/components/thisai/ModelIntro.vue'

defineOptions({
  name: '科塔智爱',
})
</script>

<template>
  <div class="ThisAi">
    <div class="Intro">
      <!-- <div class="Intro-Bg">
        <img src="/thisai/introduction.png" alt="">
        <video src="/thisai/introduction.mp4" muted autoplay loop />
    </div> -->

      <div class="Intro-Content">
        <video src="/thisai/introduction.mp4" muted autoplay loop />
        <h1>THIS AI</h1>
        <p>AI(爱)引领世界</p>
      </div>
    </div>

    <ModelIntro />
  </div>
</template>

<style>
@keyframes fadeIn {
  from {
    background-color: #fff;
  }
  to {
    background-color: #ffffffe0;
  }
}

div.ThisAi {
  position: relative;

  height: max-content;

  background-color: #f4f7fc;
}

.Intro-Content {
  z-index: 2;
  display: flex;

  flex-direction: column;
  justify-content: center;
  align-items: center;

  color: #000;

  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
  text-align: center;
  font-size: 3rem;
}

.Intro-Content h1 {
  position: absolute;
  display: flex;

  align-items: center;
  justify-content: center;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  font-size: 8rem;
  letter-spacing: 5vw;
  font-weight: 600;
  mix-blend-mode: screen;

  background-color: #fff;

  animation: fadeIn 10s 1s forwards;
}

.Intro-Content p {
  position: absolute;
  padding: 5rem 0;
  display: flex;

  align-items: flex-end;
  justify-content: center;

  left: 0;
  bottom: 0%;

  width: 100%;
  height: 100%;

  opacity: 0.75;
  color: #000;
  font-size: 2.5rem;
  letter-spacing: 1vw;
  font-weight: 600;
}

.Intro {
  position: relative;

  width: 100%;
  height: 720px;

  overflow: hidden;
}

.Intro-Bg {
  &::before {
    z-index: 1;
    content: '';
    position: absolute;

    top: 0;
    left: 0;

    width: 100%;
    height: 100%;

    background-color: #ffffffa0;
  }

  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
}

.Intro img,
.Intro video {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  opacity: 0.75;
  object-fit: cover;
}
</style>
