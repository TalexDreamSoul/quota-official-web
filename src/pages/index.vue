<script setup lang="ts">
defineOptions({
  name: 'IndexPage',
  layout: 'default',
})

const broadcast = reactive([
  {
    title: '科塔智爱 @ 全新上线',
    desc: '是智爱，也曾是挚爱',
  },
  {
    title: '科塔慧编 @ 正在研发',
    desc: '笔尖领域跨端解决方案',
  },
  {
    title: '科塔锐意 @ 正在研发',
    desc: '个人办公跨端生产力工具',
  },
  {
    title: '科塔飞讯 @ 正在研发',
    desc: '极速要闻处理生产力工具',
  },
])
</script>

<template>
  <div>
    <div class="Major">
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

    <div class="Broadcast">
      <div v-for="item in broadcast" :key="item">
        <p>{{ item.title }}</p>
        <span>{{ item.desc }}</span>
      </div>
    </div>

    <div class="Flower">
      <img src="/flower.jpg">

      <div class="Flower-Desc">
        <h1>QuotaDesign</h1>
        <span>富有淡然雅致的饱满设计.</span>
      </div>
    </div>
  </div>
</template>

<style>
.Flower-Desc {
  z-index: 1;
  position: absolute;

  left: 50%;
  top: 50%;

  color: #fff;
  font-size: 1.5rem;

  text-align: center;
  transform: translate(-50%, -50%);
}

.Flower-Desc h1 {
  font-size: 5rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  line-height: 1.5;
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

.Flower-Desc span {
  font-size: 2.5rem;
  font-weight: 400;
  line-height: 1.5;
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

.Flower {
  position: relative;
}

.Flower img {
  width: 100%;

  height: 720px;

  object-fit: cover;
}

.Broadcast {
  position: relative;

  display: flex;

  width: 100%;
  height: 140px;

  align-items: center;
  justify-content: space-around;

  background-color: #fff;
  border-top: 1px solid #f1f1f3;
  border-bottom: 1px solid #f1f1f3;
}

.Broadcast div:hover {
  cursor: pointer;
  color: #3ab8fd;
}

.Broadcast div p {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  line-height: 1.5;
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

.Broadcast div span {
  font-size: 1.25rem;
  font-weight: 400;
  line-height: 1.5;
  color: #000;
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

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
