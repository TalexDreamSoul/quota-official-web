<template>
  <div class="EmptyLayout">
    <RouterView />

    <div class="EmptyLayout__footer">
      <img src="/favicon.svg"> Powered by QuotaWish.
    </div>
  </div>
</template>

<style>
.EmptyLayout__footer img {
  width: 2.5rem;
  height: 2.5rem;
}

.EmptyLayout__footer {
  position: absolute;
  display: flex;

  bottom: 0;
  left: 0;

  width: 100%;
  padding: 1rem;

  text-align: center;
  font-size: 0.8rem;
  font-weight: 500;
  opacity: 0.5;

  justify-content: center;
  align-items: center;
}

.EmptyLayout {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  color: #000;
  overflow: hidden;
  background-color: #f4f7fc;
}

@media (prefers-color-scheme: dark) {
  .EmptyLayout {
    color: #fff;
    background-color: #1f1f1f;
  }
}
</style>
