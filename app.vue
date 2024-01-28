<template>
  <div :class="$style.root">
    <link href='https://fonts.googleapis.com/css?family=Inter' rel='stylesheet'>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<style>
body {
  margin: 0;
}
</style>

<style module>
.root {
  width: 100vw;
  height: 100vh;
}
</style>
<script setup lang="ts">
</script>
