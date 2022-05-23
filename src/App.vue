<template>
  <div id="app">
    <AppMain />
  </div>
</template>

<script>
import AppMain from "./components/AppMain.vue";

export default {
  name: "App",
  components: {
    AppMain,
  },
};
</script>

<style lang="scss">
@import "./style/style.scss";

#app {
  width: 100%;
  height: 100vh;
}
</style>
