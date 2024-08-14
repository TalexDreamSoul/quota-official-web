<script setup lang="ts">

</script>

<template>
  <div class="Swiper-Item">
    <div class="Brand">
      <div class="webgl-text webgl-fixed text-xl text-white tracking-wide" data-webgl-text-color="#ffffff">
        <img
          class="webgl-img" data-webgl-img-id="1" data-webgl-mouse-follow="1" data-webgl-mouse-offset-x="0"
          data-webgl-mouse-offset-y="0" alt="Logo" src="/favicon.svg"
        >
        科塔锐行 | 科塔智爱
      </div>
    </div>
    <div class="Title items-center justify-center">
      <div class="Content whitespace-no-wrap leading-none space-y-8">
        <div class="webgl-text text-2xl text-white" data-webgl-text-color="#ffffff">
          这是
        </div>
        <div class="webgl-text text-7xl text-white" data-webgl-text-color="#ffffff">
          强悍无边的智能助理
        </div>
      </div>
    </div>
    <div class="Swiper-Item CenterText">
      <div id="scroll-hint" class="webgl-text text-white" data-webgl-text-color="#ffffff">
        按住并拖动浏览更多
      </div>
    </div>
  </div>
</template>

<style>
.Title .Content {
  position: absolute;
  display: flex;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.Title {
  position: absolute;
  display: flex;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
}

.Brand {
  position: absolute;
  display: flex;

  gap: 0.5rem;
  align-items: center;

  top: 2.5rem;
  left: 2.5rem;
}

.Brand img {
  width: 32px;
  height: 32px;
}

.Swiper-Item .CenterText {
  position: absolute;
  display: flex;

  bottom: 1rem;

  left: 50%;
  height: 100%;

  align-items: flex-end;
  justify-content: center;

  transform: translateX(-50%);
}
</style>
