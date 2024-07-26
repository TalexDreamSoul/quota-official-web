<script setup lang="ts">
const props = defineProps<{
  title: string
  color: string
  tags: string[]
}>()

const compStyle = computed(() => {
  // 通过主色调 #xxxxxx 计算出两个颜色 一个更深 一个更浅
  const color = props.color

  const r = Number.parseInt(color.slice(1, 3), 16)
  const g = Number.parseInt(color.slice(3, 5), 16)
  const b = Number.parseInt(color.slice(5, 7), 16)

  const darkerColor = `rgb(${Math.max(r - 50, 0)}, ${Math.max(g - 50, 0)}, ${Math.max(b - 50, 0)})`
  const lighterColor = `rgb(${Math.min(r + 50, 255)}, ${Math.min(g + 50, 255)}, ${Math.min(b + 50, 255)})`

  return `--c: ${color};--dc: ${darkerColor};--lc: ${lighterColor};--sc: ${color}80`
})
</script>

<template>
  <div :style="compStyle" class="ModelBoxItem">
    <div class="logo">
      <img src="/thisai/logo.png">
    </div>
    <h2>{{ title }}</h2>
    <p class="TagContainer">
      <span v-for="tag in tags" :key="tag" class="tag" v-text="tag" />
    </p>

    <div class="desc" my-8>
      <slot />
    </div>
  </div>
</template>

<style scoped>
@media (max-width: 768px) {
  .TagContainer {
    display: none;
  }

  .desc {
    display: none;
  }
}

.TagContainer {
  text-align: left;
}

.desc {
  color: #fff;
  text-align: left;

  font-size: 18px;
}
.tag {
  margin-left: 0.25rem;
  margin-right: 0.5rem;
  padding: 0.25rem 0.5rem;

  color: #fff;
  font-size: 16px;
  border-radius: 6px;
  border: 1px solid #fff;
}

.ModelBoxItem h2 {
  color: #fff;
  text-align: left;
  font-size: 2.5rem;
}

.ModelBoxItem .logo {
  width: 64px;
  height: 64px;

  border-radius: 12px;
  background-color: #ffffff30;
  backdrop-filter: blur(18px);

  box-shadow: #ffffff30 0 0 4px 1px;
}

.ModelBoxItem .logo img {
  width: 64px;
  height: 64px;
}

.ModelBoxItem {
  padding: 3rem;

  width: 50%;
  min-width: 200px;
  max-width: 600px;
  height: 340px;

  position: relative;

  border-radius: 16px;
  box-sizing: border-box;
  background-image: linear-gradient(120deg, var(--lc) 0%, var(--c) 100%);
}
</style>
