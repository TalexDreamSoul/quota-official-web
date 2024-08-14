<script setup lang="ts">

</script>

<template>
  <div class="SliderAnnounce Swiper-Item">
    <div class="ImageBlock left-0 top-0">
      <img
        class="webgl-img h-screen w-screen" data-webgl-img-id="2" data-webgl-mouse-follow="1"
        data-webgl-mouse-offset-x="-0.2" data-webgl-mouse-offset-y="0"
        src="/ai-chip2.jpg" crossorigin="anonymous" alt=""
      >
    </div>
    <div class="TextBlock">
      <div class="whitespace-no-wrap flex flex-col items-start leading-none space-y-8">
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          Fantasy & Incrediable
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          超乎想象的快,准
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          有广度,宽度,深度的智能
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          有温度,精度,速度的智能
        </div>
        <div class="webgl-text text-3xl text-white" data-webgl-text-color="#ffffff">
          立即开始永久免费使用
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.SliderAnnounce .TextBlock {
  z-index: 1;
  position: absolute;
  display: flex;

  align-items: center;

  /* width: 50%; */
  height: 100%;

  right: 20%;
}

.ImageBlock {
  position: absolute;
}
/* .SliderAnnounce .ImageBlock img {
  height: 100%;
}

.SliderAnnounce .TextBlock {
  display: flex;

  align-items: center;

  width: 50%;
  height: 100%;
}

.SliderAnnounce {
  position: absolute;
  padding: 10rem 4rem;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  gap: 5rem;
  display: flex;

  align-items: center;
  justify-content: space-around;
} */
</style>
