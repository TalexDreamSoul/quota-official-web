<script setup lang="ts">
const router = useRouter()
</script>

<template>
  <header>
    <div flex flex-1 cursor-pointer items-center justify-center class="logo" @click="router.push('/')">
      <img src="/favicon.svg" alt="logo">
      <h1 text-1em font-bold>
        科塔锐行
      </h1>
    </div>

    <div class="header-nav-bar nav" w="40%" content="space-between" flex flex-1 justify-between gap-6>
      <span cursor-pointer hover:op-75 @click="router.push('/thisai')">科塔智爱</span>
      <span cursor-pointer hover:op-75>科塔慧编</span>
      <span cursor-pointer hover:op-75>科塔锐意</span>
      <span cursor-pointer hover:op-75>科塔飞讯</span>
      <span cursor-pointer hover:op-75>科塔开放</span>
    </div>

    <div class="header-nav-personal personal" mr-2 flex flex-1 items-center justify-center text-right text-1.125rem>
      注册 | 登录
    </div>
  </header>
</template>

<style>
@media (max-width: 768px) {
  .header-nav-bar,
  .header-nav-personal {
    display: none;
  }
}

header .logo img {
  width: 72px;
  height: 72px;
}

header {
  padding: 0 5rem;
  display: flex;

  font-size: 20px;

  color: #000;
  align-items: center;
  justify-content: space-around;
}
</style>
