<script setup lang="ts">

</script>

<template>
  <footer>
    <div flex items-center class="logo">
      <img src="/favicon.svg">
      <h1 text-2xl font-bold>
        QuotaWish
      </h1>
    </div>
    <div flex class="info">
      <!-- 声明公司已注册，放备案内容 -->
      <div>
        Copyright © 2024 QuotaWish Inc.
      </div>
      <div>
        <a href="https://beian.miit.gov.cn/" target="_blank">蜀ICP备2024090189号</a>
      </div>
    </div>
  </footer>
</template>

<style>
div.logo,
div.logo img {
  width: 128px;
  height: 128px;
}

div.info {
  display: flex;
  justify-content: flex-start;
}

div.info > div {
  padding: 0 0.5rem;

  border-right: 2px solid #cfcdcd;
}

div.info > div:last-child {
  border-right: none;
}

footer {
  position: relative;
  display: flex;

  left: 50%;

  align-items: center;
  justify-content: space-around;

  width: 100%;
  height: 200px;

  background-color: #f5f5f5;
  padding: 20px;
  text-align: center;

  transform: translateX(-50%);
}
</style>
