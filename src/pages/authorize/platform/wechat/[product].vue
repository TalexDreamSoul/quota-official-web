<script setup lang="ts">
// defineOptions({
//   name: 'ProductAuthorize',
//   layout: 'empty',
// })

const route = useRoute()

const uaAvailable = computed(() => navigator.userAgent.toLowerCase().includes('wechat'))
const product = computed(() => route.params.product as string)

const queryAvailable = computed(() => route.query.code && route.query.state)

const response = ref<any>()
const ignoreEnv = ref(false)
async function authorize() {
  if (response.value)
    return

  const url = `https://api.quotawish.com/api/platform/qrcode/auth/wechat?code=${route.query.code}&state=${route.query.state}`

  try {
    const res = await fetch(url)
    const data = await res.json()

    response.value = data

    console.log('data', data)
  }
  catch (error) {
    console.error(error)
  }
}

const success = computed(() => response.value?.message === 'success')
</script>

<template>
  <div class="PlatForm">
    <div v-if="product === 'thisai'" class="PlatForm-Dialog">
      <template v-if="!uaAvailable && !ignoreEnv">
        <div class="icon">
          <div i-carbon:face-dissatisfied />
        </div>
        <p>微信环境不安全</p>

        <button class="warn" my-6 @click="ignoreEnv = true">
          继续授权
        </button>
      </template>
      <template v-else-if="!queryAvailable">
        <div class="icon">
          <div i-carbon:checkmark-filled-error />
        </div>
        <p>无法完成授权</p>

        <button class="error" my-6>
          授权参数错误
        </button>
      </template>
      <template v-else>
        <div class="icon">
          <div i-carbon:devices />
        </div>
        <p v-if="response">
          {{ success ? '授权成功' : '授权失败' }}
          <span v-if="!success">({{ response }})</span>
        </p>
        <p v-else>
          等待授权
        </p>

        <button v-if="!response" my-6 @click="authorize">
          {{ success ? '您已成功登录 科塔智爱' : '点击授权登录' }}
        </button>
      </template>
    </div>
    <div v-else class="PlatForm-Dialog">
      <div class="icon">
        <div i-carbon:close-outline />
      </div>
      <p>无法完成授权</p>

      <button class="error" my-6>
        不支持当前平台授权
      </button>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: empty
</route>

<style>
  .PlatForm-Dialog button {
  padding: 0.25rem 0.75rem;

  font-size: 1.125rem;
  font-weight: normal;

  border-radius: 14px;
  background-color: #3dc3ff;
  box-shadow: 0 0 12px #3dc3ff;
}

.PlatForm-Dialog button.error {
  background-color: #f04e48;
  box-shadow: 0 0 12px #f04e48;
}

.PlatForm-Dialog button.warn {
  background-color: #e78248;
  box-shadow: 0 0 12px #e78248;
}

.PlatForm-Dialog .icon {
  padding: 0.5rem;

  border-radius: 16px;
  background-color: #fff5;
}

.PlatForm-Dialog {
  position: relative;
  display: flex;

  gap: 1rem;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  width: 100%;
  height: 100%;

  font-size: 1.5rem;
  font-weight: bold;
}

.PlatForm {
  padding: 1rem;

  height: 100%;
}
</style>
