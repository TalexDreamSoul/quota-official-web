<script setup lang="ts">

</script>

<template>
  <div class="SliderIntro Swiper-Item">
    <div class="ImageBlock">
      <img
        class="webgl-img h-screen w-screen" data-webgl-img-id="1" data-webgl-mouse-follow="1"
        data-webgl-mouse-offset-x="0" data-webgl-mouse-offset-y="0" src="/breath.jpg" crossorigin="anonymous" alt=""
      >
    </div>
    <div class="TextBlock">
      <div class="whitespace-no-wrap flex flex-col items-start leading-none space-y-8">
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          专注于学习,办公,生活体验
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          不可思议的模态能力
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          令人惊叹的饱满设计
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          生命韵律与效率工具
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          强悍无边的全新体验
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.SliderIntro .TextBlock {
  z-index: 1;
  position: absolute;
  display: flex;

  align-items: center;

  /* width: 50%; */
  height: 100%;

  left: 20%;
}

.SliderIntro .ImageBlock {
  position: absolute;
}
/* .SliderIntro .ImageBlock img {
  height: 100%;
}

.SliderIntro .TextBlock {
  display: flex;

  align-items: center;

  width: 50%;
  height: 100%;
}

.SliderIntro {
  position: absolute;
  padding: 10rem 4rem;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  gap: 5rem;
  display: flex;

  align-items: center;
  flex-direction: row-reverse;
  justify-content: space-around;
} */
</style>
