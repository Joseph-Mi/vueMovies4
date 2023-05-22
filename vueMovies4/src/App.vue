<script setup>
import Movies from "./components/Movies.vue";
</script>

<template>
   <div class="app-container">
    <Suspense>
      <Movies />
    </Suspense>
  </div>
</template>

<style scoped>
</style>