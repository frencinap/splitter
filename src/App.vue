<template>
  <div id="app">
    <Tips />
  </div>
</template>

<script>
import Tips from "./components/Tips.vue";

export default {
  name: "App",
  components: {
    Tips,
  },
};
</script>

<style>
#app {
  font-family: "Space Mono", monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: hsl(185, 41%, 84%);
  text-align: center;
  display: flex;
  flex-flow: column;
  align-items: center;
  vertical-align: middle;
}
</style>
