<script name="TouchMenu" lang="ts" setup>
const pointer = ref<HTMLElement>()

provide('changePointer', (el: HTMLElement) => {
  nextTick(() => fixPointer(el))
})

async function fixPointer(targetEl: HTMLElement) {
  const pointerEl = pointer.value
  if (!pointerEl || !targetEl)
    return

  const pointerStyle = pointerEl.style

  const pointerRect = pointerEl.getBoundingClientRect()
  const nodeRect = targetEl.getBoundingClientRect()

  const diffTop = -targetEl.parentElement!.offsetLeft /* + nodeRect.width */ + 4

  if (nodeRect.left > pointerRect.left) {
    pointerStyle.width = `${nodeRect.width * 0.8}px`
    pointerStyle.transition = 'all 0'
    pointerStyle.opacity = '0'

    await sleep(100)

    pointerStyle.left = `${nodeRect.left + diffTop}px`

    await sleep(100)

    pointerStyle.transition = 'all .25s'
    pointerStyle.opacity = '1'

    await sleep(100)

    pointerStyle.left = `${nodeRect.left + (nodeRect.width * 0.2) + diffTop}px`
    pointerStyle.width = `${nodeRect.width * 0.6}px`
  }
  else {
    pointerStyle.transform = `translate(-${nodeRect.width * 0.2}px, 0)`
    pointerStyle.width = `${nodeRect.width * 0.8}px`

    await sleep(100)

    pointerStyle.transition = 'all 0'
    pointerStyle.opacity = '0'

    await sleep(100)
    pointerStyle.transform = ''
    pointerStyle.left = `${nodeRect.left + (nodeRect.width * 0.2) + diffTop}px`

    await sleep(100)

    pointerStyle.transition = 'all .25s'
    pointerStyle.opacity = '1'

    await sleep(100)

    pointerStyle.width = `${nodeRect.width * 0.6}px`
  }
}

onMounted(() => {
  setTimeout(() => {
    const dom = document.querySelector('.TouchMenuItem-Container.active') as HTMLElement

    if (dom)
      fixPointer(dom)
  }, 500)
})
</script>

<template>
  <div relative box-border h-full w-full justify-between>
    <slot />
    <div ref="pointer" h="3px" transition=".25s" absolute border-rounded opacity-0 class="top-[100%] bg-[#3AB8FD]" />
  </div>
</template>

<style lang="scss"></style>
