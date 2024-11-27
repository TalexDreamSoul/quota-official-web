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

    <div class="header-nav-bar nav" w="45%" content="space-between" flex flex-1 justify-between gap-6 text-2.5>
      <TSelect flex flex-row>
        <TSelectItem route="" name="index">
          首页
        </TSelectItem>
        <TSelectItem route="thisai" name="thisai">
          科塔智爱
        </TSelectItem>
        <TSelectItem name="edit">
          科塔慧编
        </TSelectItem>
        <TSelectItem name="touch">
          科塔锐意
        </TSelectItem>
        <TSelectItem name="im">
          科塔飞讯
        </TSelectItem>
        <TSelectItem name="open">
          科塔开放
        </TSelectItem>
      </TSelect>
    </div>

    <div class="header-nav-personal personal" mr-2 flex flex-1 cursor-pointer items-center justify-center text-right text-2.5 hover:op-50>
      注册 | 登录
    </div>
  </header>
</template>

<style>
@media screen and (max-width: 1080px) {
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

  /* color: #fff; */
  align-items: center;
  justify-content: space-around;
}
</style>
