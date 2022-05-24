<template>
  <div class="logo-container" v-if="isFlagAvailable(this.flagLanguage)">
    <img :src="this.language" :alt="thisFlag(this.flagLanguage)" />
  </div>
  <div v-else>
    <h3>{{ this.flagLanguage }}</h3>
  </div>
</template>

<script>
export default {
  name: "AppFlags",
  props: {
    flagLanguage: String,
  },
  data() {
    return {
      language: "",
    };
  },
  methods: {
    thisFlag(thisLanguage) {
      if (thisLanguage == "en") {
        this.language = require("../assets/img/english.png");
      } else if (thisLanguage == "it") {
        this.language = require("../assets/img/italy.png");
      } else if (thisLanguage == "es") {
        this.language = require("../assets/img/spain.png");
      } else if (thisLanguage == "de") {
        this.language = require("../assets/img/germany.png");
      }
    },
    isFlagAvailable(thisLanguage) {
      if (thisLanguage == "en") {
        return true;
      } else if (thisLanguage == "it") {
        return true;
      } else if (thisLanguage == "es") {
        return true;
      } else if (thisLanguage == "de") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
$text-color: #727873;

.logo-container {
  width: 1.2rem;
  margin-right: auto;
}
h3 {
  margin: 0;
  font-size: 0.8rem;
  font-weight: 300;
  text-align: start;
  color: $text-color;
}
</style>
