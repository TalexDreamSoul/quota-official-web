<script setup>
// 获取 page meta
const route = useRoute()

watch(() => route.value, () => {
  console.log('r', route)
}, { immediate: true })
</script>

<template>
  <main
    class="DefaultLayout"
  >
    <Header v-if="!route.meta.layout" />
    <RouterView />

    <Footer v-if="!route.meta.layout" />
  </main>
</template>

<style>
.DefaultLayout > header {
  z-index: 10;
  position: sticky;

  top: 0;
  left: 0;

  width: 100%;
  height: 80px;

  background-color: #ffffffa0;
  border-bottom: 1px solid #f1f1f3;
  backdrop-filter: blur(18px) saturate(180%);
}

main.DefaultLayout {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  background-color: #f4f7fc;
}
</style>
