<script setup lang="ts">
import NavBar from "@/components/NavBar.vue";
</script>

<template>
  <strong>Current route path:</strong> {{ $route.fullPath }}

  <NavBar />
  <RouterView />
</template>
