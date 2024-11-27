<script setup>
// 获取 page meta
const route = useRoute()

watch(() => route.value, () => {
  console.log('r', route)
}, { immediate: true })

const fullScreenPage = ['/thisai']

const hide = computed(() => fullScreenPage.filter(item => route.fullPath.startsWith(item))?.length)
</script>

<template>
  <main
    class="DefaultLayout"
  >
    <Header v-if="!hide" />
    <RouterView />

    <Footer v-if="!hide" />
  </main>
</template>

<style>
.DefaultLayout > header {
  z-index: 10;
  position: sticky;

  top: 0;
  left: 0;

  width: 100%;
  height: 64px;

  /* background-color: #101010a0; */
  /* border-bottom: 1px solid #161616; */
  backdrop-filter: blur(18px) saturate(180%);
}

main.DefaultLayout {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  /* background-color: #262626; */
}
</style>
