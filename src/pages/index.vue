<script setup>
import {computed, ref} from 'vue'
import { useDisplay } from 'vuetify'
const display = useDisplay();
const isMobile = computed(() => display.smAndDown.value)
</script>

<template>
<div class="my_main">
  <div class="banner">
    <div class="bg"></div>
  </div>
  <div class="my_text mb-4">
    <h1 class="text-center" :class="!isMobile ? 'mt-n14': ''">Região de Crescimento e Prosperidade</h1>
    <p class="mt-2">A zona oeste de Poços de Caldas é uma região de beleza, prosperidade e possibilidades</p>
    <p>Esse portal é uma ponte para que você conheça melhor, perceba potenciais e possibilidades que
    melhorem e te ajudem em várias áreas da sua vida</p>
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
  .my_text {
    padding: 1%;
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
    .my_text {
      margin-top: 37%;
      padding: 2.8%;
      h1{
        font-size: 1.4rem;
      }
    }
  }
}
</style>