<script setup lang="ts">
  const url = useRequestURL()
  const pathname = url.pathname.replace('/', '')
</script>

<template>
  <p>URL is: {{ url }}</p>
  <p>Path is: {{ pathname }}</p>
</template>
