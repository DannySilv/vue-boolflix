<template>
  <div id="app">
    <AppHeader />
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";

export default {
  name: "App",
  components: {
    AppHeader,
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
