<script setup lang="ts">

</script>

<template>
  <div h-full>
    <div class="major-inner" />

    <div class="Major-Desc">
      <h1>科塔锐行 | ThisAI</h1>
      <p my-4>
        有温度、精度、速度 | 有厚度、密度、广度
      </p>
    </div>

    <div class="Major-Button">
      <button>了解更多</button>
    </div>
  </div>
</template>

<style>
.Major-Button {
  position: absolute;

  left: 50%;
  bottom: 30%;

  transform: translate(-50%, -50%);
}

.Major-Button button:hover {
  background-color: #fff;
  color: #000;
  border: 1px solid #fff;

  border-radius: 1rem;
}

.Major-Button button {
  padding: 0.75rem 1.5rem;

  color: #000;
  background-color: #ffffff50;
  border: 1px solid #fff;
  border-radius: 0.75rem;

  cursor: pointer;
  backdrop-filter: blur(18px);

  transition: all 0.2s ease-in-out;
}

.Major {
  position: relative;

  width: 100%;
  height: 720px;
}

.Major-Desc h1 {
  font-weight: 600;
}

.Major-Desc p {
  opacity: 0.75;

  max-width: 80%;

  font-size: 1.5rem;
}

.Major-Desc {
  position: relative;
  display: flex;

  top: 30%;
  left: 50%;

  align-items: center;
  justify-content: center;
  flex-direction: column;

  font-size: 2rem;

  mix-blend-mode: soft-light;
  transform: translate(-50%, -50%);
}

.major-inner {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  opacity: 0.5;
  background-size: contain;
  background-image: radial-gradient(
      at 63% 60%,
      hsla(58, 87%, 62%, 0.3) 0,
      hsla(58, 87%, 62%, 0) 50%
    ),
    radial-gradient(
      at 58% 33%,
      hsla(59, 91%, 69%, 0.1) 0,
      hsla(59, 91%, 69%, 0) 50%
    ),
    radial-gradient(
      at 47% 17%,
      hsla(144, 90%, 59%, 0.3) 0,
      hsla(144, 90%, 59%, 0) 50%
    ),
    radial-gradient(
      at 34% 17%,
      hsla(233, 93%, 59%, 0.75) 0,
      hsla(233, 93%, 59%, 0) 50%
    ),
    radial-gradient(
      at 43% 43%,
      hsla(338, 92%, 59%, 0.2) 0,
      hsla(338, 92%, 59%, 0) 50%
    ),
    radial-gradient(
      at 34% 68%,
      hsla(255, 92%, 56%, 0.3) 0,
      hsla(255, 92%, 56%, 0) 50%
    ),
    radial-gradient(
      at 6% 8%,
      hsla(260, 88%, 54%, 0.3) 0,
      hsla(260, 88%, 54%, 0) 50%
    );

  animation: hue 10s infinite linear;
}

@keyframes hue {
  0% {
    filter: hue-rotate(0deg);
  }

  100% {
    filter: hue-rotate(360deg);
  }
}
</style>
