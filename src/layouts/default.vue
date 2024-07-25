<template>
  <main
    class="DefaultLayout"
  >
    <Header />
    <RouterView />

    <Footer />
  </main>
</template>

<style>
.DefaultLayout > header {
  z-index: 1;
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
