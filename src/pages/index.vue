<script setup lang="ts">
import { A11y, Autoplay, Controller, EffectCreative, Navigation, Pagination, Scrollbar } from 'swiper/modules'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/css'
import 'swiper/css/autoplay'
import 'swiper/css/effect-creative'
import 'swiper/css/controller'
import 'swiper/css/navigation'
import 'swiper/css/pagination'
import 'swiper/css/scrollbar'

defineOptions({
  name: 'IndexPage',
  layout: 'default',
})

const broadcast = reactive([
  {
    title: '科塔智爱 @ 全新上线',
    desc: '更有效率、更准确的AI',
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
      <Swiper
        :autoplay="{ delay: 3000, disableOnInteraction: true }"
        navigation :pagination="{ clickable: true }" :scrollbar="{ draggable: true }"
        :modules="[EffectCreative, Controller, Autoplay, Navigation, Pagination, Scrollbar, A11y]" effect="creative"
      >
        <SwiperSlide>
          <AiProduct />
        </SwiperSlide>
        <SwiperSlide>
          <TouchProduct />
        </SwiperSlide>
      </Swiper>
    </div>

    <div py-4 class="Broadcast">
      <div v-for="item in broadcast" :key="item.title">
        <p>{{ item.title }}</p>
        <span>{{ item.desc }}</span>
      </div>
    </div>

    <div class="Flower">
      <img src="/flower.jpg">

      <div class="Flower-Desc">
        <h1><img src="/design-logo.png" alt="logo"></h1>
        <span>富有淡然雅致的饱满设计.</span>
      </div>
    </div>
  </div>
</template>

<style>
.Flower-Desc {
  z-index: 1;
  position: absolute;
  display: flex;

  left: 50%;
  top: 50%;

  /* color: #fff; */
  font-size: 1.5rem;

  align-items: center;
  flex-direction: column;

  text-align: center;
  transform: translate(-50%, -50%);
}

.Flower-Desc h1 {
  img {
    position: relative;
    left: 10%;

    width: 80%;
    height: 200px;
    object-fit: contain;

    opacity: 0.85;
    filter: brightness(200%) invert(0.95);
  }
  max-width: 80%;
  text-overflow: ellipsis;

  font-size: 5rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
  line-height: 1.5;
}

.Flower-Desc span {
  font-size: 2.5rem;
  font-weight: 600;
  line-height: 1.5;

  background: -webkit-linear-gradient(345deg, #a9b3cd 25%, #647eff);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.Flower {
  position: relative;

  color: #fff;
}

.Flower img {
  width: 100%;

  height: 720px;

  object-fit: cover;
}

.Broadcast {
  position: relative;

  display: flex;
  flex-wrap: wrap;

  width: 100%;
  min-height: 140px;

  align-items: center;
  justify-content: space-around;

  /* color: #fff; */
  background-color: #fff;
  border-top: 1px solid #262626;
  border-bottom: 1px solid #262626;
}

.Broadcast div:hover {
  cursor: pointer;
  color: #3ab8fd;
}

.Broadcast div {
  margin: 1rem;
}

.Broadcast div p {
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 0.125rem;
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

.Broadcast div span {
  font-size: 20px;
  font-weight: 400;
  /* color: #fff; */
  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}

div.swiper,
.swiper-wrapper,
.swiper-slide {
  height: 100%;

  background-color: #efefef;
}
</style>
