<script setup lang="ts">

</script>

<template>
  <header>
    <div flex flex-1 items-center class="logo">
      <img src="/favicon.svg" alt="logo">
      <h1 text-1em font-bold>
        科塔锐行
      </h1>
    </div>

    <div w="40%" content="space-between" flex flex-1 justify-between gap-6 class="nav">
      <span cursor-pointer hover:op-75>科塔智爱</span>
      <span cursor-pointer hover:op-75>科塔慧编</span>
      <span cursor-pointer hover:op-75>科塔锐意</span>
      <span cursor-pointer hover:op-75>科塔飞讯</span>
      <span cursor-pointer hover:op-75>科塔开放</span>
    </div>

    <div mr-2 flex-1 text-right text-1.125rem class="personal">
      注册 | 登录
    </div>
  </header>
</template>

<style>
header .logo img {
  width: 72px;
  height: 72px;
}

header {
  padding: 0 5rem;
  display: flex;

  font-size: 20px;

  align-items: center;
  justify-content: space-between;
}
</style>
