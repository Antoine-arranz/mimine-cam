<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'

const stream = ref(null)
const constraints = {
  audio: false,
  video: {
    width: { min: 1024, ideal: 1280, max: 1920 },
    height: { min: 576, ideal: 720, max: 1080 },
    facingMode: 'environment',
  },
}

onMounted(async () => {
  stream.value = await navigator.mediaDevices.getUserMedia(constraints)
})

onBeforeUnmount(() => {
  stream.value.getTracks().forEach(track => track.stop())
})
</script>

<template>
  <video :srcObject="stream" width="1000" height="1000" autoplay></video>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
