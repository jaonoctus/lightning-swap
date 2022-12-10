<script setup lang="ts">
import { RouterView } from "vue-router";
</script>

<template>
  <div class="container">
    <RouterView />
  </div>
</template>

<style scoped>
.container {
  background-color: #141414;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: #2e3336 0px 54px 55px, #2e3336 0px -12px 30px, #2e3336 0px 4px 6px,
    #2e3336 0px 12px 13px, #2e3336 0px -3px 5px;
}
</style>
