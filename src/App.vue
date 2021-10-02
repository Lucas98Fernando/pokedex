<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style lang="scss" scoped>
#app {
  background: rgb(102, 155, 188);
  background: radial-gradient(
    circle,
    rgba(102, 155, 188, 1) 0%,
    rgba(255, 77, 109, 1) 100%
  );
}
</style>
