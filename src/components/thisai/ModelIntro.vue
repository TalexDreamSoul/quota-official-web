<script setup lang="ts">

</script>

<template>
  <div class="ModelIntro">
    <h1>QuotaGPT</h1>
    <p>有温度、精度、速度 | 有厚度、密度、广度</p>

    <div my-8 flex flex-wrap items-center justify-center gap-4 class="ModelBox">
      <ModelBox :tags="['128k上下文', '自推理工具能力']" color="#8E4BFF" title="科塔通用模型 Pro">
        科塔锐行最新推出的专业版LLM模型，具备高达128K的长文本处理能力，展现出卓越的理解、生成与逻辑推理综合能力。该模型灵活适用于多种应用场景，包括问答、内容总结、创作以及分类等，满足多样化的需求。
      </ModelBox>
      <ModelBox :tags="['秒级响应', '上下文检索']" color="#133C9A" title="科塔通用模型 Lite">
        科塔锐行最新推出的轻量版LLM模型，相较于专业版，显著降低了成本与响应延迟，旨在为用户提供更加灵活的模型选择，以满足不同应用场景的需求。上下文检索能力更强，拥有片段自总结响应能力。
      </ModelBox>
    </div>
  </div>
</template>

<style>
.ModelBox {
  position: relative;

  left: 10%;
  width: 80%;
}

.ModelIntro h1 {
  font-size: 5rem;
  font-weight: 600;
  line-height: 1.5;

  color: #000;
}

.ModelIntro p {
  font-size: 1.5rem;
  font-weight: 400;
  line-height: 1.5;

  color: #000;
}

.ModelIntro {
  position: relative;
  padding: 5% 0;
  display: flex;

  width: 100%;
  height: 800px;

  flex-direction: column;
  justify-content: center;

  color: #000;
  text-align: center;

  font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
}
</style>
