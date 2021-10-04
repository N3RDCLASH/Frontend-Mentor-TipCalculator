<script setup>
import Calculator from "./components/Calculator/Calculator.vue";
console.log("test");
</script>

<template>
  <Calculator />
</template>

<style>
:root {
  --font: "Space Mono", monospace;
}
body {
  background-color: hsl(185, 41%, 84%);
  font-family: var(--font) !important;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
