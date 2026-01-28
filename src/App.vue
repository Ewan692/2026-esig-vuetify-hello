<template>
  <h1>{{ message }}</h1>
  <input v-model="message" type="text">
</template>

<script setup>
  const message = ref('Hello there !')
</script>
