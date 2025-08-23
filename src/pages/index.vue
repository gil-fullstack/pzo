<script setup>
</script>

<template>
<div class="my_main">
  <div class="banner">
    <div class="bg"></div>
  </div>
  <div class="my_text mt-7">
    <h1>Região de Crescimento e Prosperidade</h1>
  </div>
</div>
</template>

<style lang="scss" scoped>
.my_main {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  padding: 0;
  height: 100%;

  .banner {
    width: 100%;
    height: 100%;
    min-height: 100vh;
    min-width: 100vh;

    .bg {
      position: absolute;
      background-image: url('../assets/prefeitura5.jpg');
      background-size: cover;
      background-position: center;
      min-height: 100%;
      max-height: 100%;
      inset: 0;
      z-index: 1;
    }
  }
}

@media (max-width: 768px) {
  .my_main {
    .banner {
      min-height: auto;
      margin-top: 21%;
      .bg {
        margin-top: 14%;
        background-image: url('../assets/prefeitura5.jpg');
        background-size: 100%;
        background-position: top;
        min-height: 50%;
        max-height: 100%;
        max-width: 100%;
        inset: 0;
      }
    }
  }
}
</style>