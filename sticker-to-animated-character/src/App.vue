<script setup>
import ImageUpload from './components/ImageUpload.vue'
</script>

<template>
  <header>
    <h1>Sticker to Animated Character</h1>
    <p>Upload your sticker to start the animation process.</p>
  </header>

  <main>
    <ImageUpload />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    flex-direction: column;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }
}
</style>
