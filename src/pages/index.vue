<script setup lang="ts">
import { Autoplay, Controller, EffectCreative } from 'swiper/modules'
import { Swiper, SwiperSlide } from 'swiper/vue'
import 'swiper/css'
import 'swiper/css/autoplay'
import 'swiper/css/effect-creative'
import 'swiper/css/controller'

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
      <Swiper :modules="[EffectCreative, Controller, Autoplay]" effect="creative">
        <SwiperSlide>
          <AiProduct />
        </SwiperSlide>
        <SwiperSlide>
          <AiProduct />
        </SwiperSlide>
      </Swiper>
    </div>

    <div class="Broadcast">
      <div v-for="item in broadcast" :key="item.title">
        <p>{{ item.title }}</p>
        <span>{{ item.desc }}</span>
      </div>
    </div>

    <div class="Flower">
      <img src="/flower.jpg">

      <div class="Flower-Desc">
        <h1><span>QuotaDesign</span></h1>
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
  max-width: 80%;
  text-overflow: ellipsis;

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
  flex-wrap: wrap;

  width: 100%;
  min-height: 140px;

  align-items: center;
  justify-content: space-around;

  color: #000;
  background-color: #fff;
  border-top: 1px solid #f1f1f3;
  border-bottom: 1px solid #f1f1f3;
}

.Broadcast div:hover {
  cursor: pointer;
  color: #3ab8fd;
}

.Broadcast div {
  margin: 1rem;
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

div.swiper,
.swiper-wrapper,
.swiper-slide {
  height: 100%;
}
</style>
